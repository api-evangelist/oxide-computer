---
name: oxide-provision-instance
description: Provision a VM instance on an Oxide rack from an image, attach storage and networking, and start it — using the Oxide Region API.
generated: '2026-08-26'
method: generated
source: openapi/oxide-computer-region-api-openapi.json
api: Oxide Region API
base_url: https://{oxide-control-plane-host}
operations:
  - project_list
  - project_create
  - image_list
  - instance_create
  - instance_view
  - instance_start
  - instance_stop
  - instance_disk_attach
  - instance_external_ip_list
---

# Provision an instance on Oxide

## Before you act

- **There is no vendor host.** The Oxide API runs on the customer's own rack. You must be told the
  control-plane host (`OXIDE_HOST`, or `oxide auth login --host https://...`). Never guess it.
- **Auth** is `Authorization: Bearer <device token>` (`OXIDE_TOKEN`). See
  `authentication/oxide-computer-authentication.yml`.
- **Send `api-version`.** Without the header your request targets whatever version the rack is on
  now, so a control-plane upgrade can change behaviour underneath you.
- **There is no idempotency key.** If a create times out, do **not** blindly retry. Call
  `instance_view` (or `instance_list` with the project selector) first and check whether your named
  instance already exists. Names are unique within a project, so a blind retry produces a conflict,
  not a duplicate — but you cannot tell a conflict you caused from one someone else caused.
- **There is no dry run** on any write operation.

## Steps

1. **Find or create the project.** `project_list` (`GET /v1/projects`). If the target project does
   not exist, `project_create` (`POST /v1/projects`).
2. **Pick an image.** `image_list` (`GET /v1/images?project=<project>`) returns project images;
   silo-promoted images are visible too. Record the image `id` or `name`.
3. **Create the instance.** `instance_create` (`POST /v1/instances?project=<project>`). The body
   carries the name, description, ncpus, memory, boot disk source, and optionally network
   interfaces, external IPs and SSH public keys. Note that Oxide's own CLI wraps this as
   `oxide instance from-image`.
4. **Confirm.** `instance_view` (`GET /v1/instances/{instance}?project=<project>`) until the run
   state settles. Provisioning is asynchronous — a 201 means accepted, not running.
5. **Attach anything not supplied at create time.** `instance_disk_attach`
   (`POST /v1/instances/{instance}/disks/attach`) for additional disks;
   `instance_external_ip_list` to see what external addressing landed.
6. **Start it if it was created stopped.** `instance_start`
   (`POST /v1/instances/{instance}/start`).

## Undoing this

`instance_stop` reverses `instance_start`. `instance_disk_detach` reverses
`instance_disk_attach`. `instance_delete` is **terminal** — Oxide publishes no undelete and no
retention window. If the instance holds data you care about, take `snapshot_create` on its disks
first; restoring from a snapshot is the only documented recovery path.

## Errors

The envelope is `{message, request_id, error_code}` — not RFC 9457. `422` means the payload parsed
but broke a domain rule (name collision, quota, invalid CIDR): read `message`. `404` can mean
"not authorized to see it" as well as "not there". Quote `request_id` in any support case; a
support bundle (`support_bundle_create`) collects the correlating control-plane state.

## Rate limits

None published, and the API declares no `429` and no rate-limit headers. Do not assume you may
hammer it — this is one rack, not a hyperscaler fleet.
