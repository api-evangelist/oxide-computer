---
name: oxide-manage-storage
description: Create, attach, snapshot and restore Oxide disks, and turn a snapshot into a new disk or image.
generated: '2026-08-26'
method: generated
source: openapi/oxide-computer-region-api-openapi.json
api: Oxide Region API
base_url: https://{oxide-control-plane-host}
operations:
  - disk_list
  - disk_view
  - disk_create
  - disk_delete
  - instance_disk_attach
  - instance_disk_detach
  - snapshot_list
  - snapshot_create
  - snapshot_view
  - snapshot_delete
  - image_create
  - image_promote
  - image_demote
  - disk_bulk_write_import_start
  - disk_bulk_write_import_stop
---

# Manage Oxide storage

## The one thing to know first

**Snapshots are the only reversal Oxide gives you for data.** There is no undelete for a disk, no
retention window, and no restore operation. `disk_delete` is terminal. Take `snapshot_create`
*before* any destructive change, not after.

## Steps

1. **Inventory.** `disk_list` (`GET /v1/disks?project=<project>`), `snapshot_list`
   (`GET /v1/snapshots?project=<project>`). Both are cursor-paginated: pass `limit` and follow
   `next_page` from the `*ResultsPage` envelope.
2. **Create a disk.** `disk_create` (`POST /v1/disks?project=<project>`). The disk source may be
   blank, an image, or a snapshot — restoring is expressed as "create a disk whose source is a
   snapshot", not as a `restore` call.
3. **Attach / detach.** `instance_disk_attach` and `instance_disk_detach`
   (`POST /v1/instances/{instance}/disks/attach|detach`). Detach is a clean reversal of attach.
4. **Snapshot.** `snapshot_create` (`POST /v1/snapshots?project=<project>`) takes a point-in-time
   copy. Confirm with `snapshot_view` before you rely on it.
5. **Import an external image.** `disk_bulk_write_import_start`, write the chunks, then
   `disk_bulk_write_import_stop`. If an import goes wrong, `disk_bulk_write_import_stop` is the
   documented way out of the import state.
6. **Publish an image.** `image_create`, then `image_promote` to make it visible silo-wide.
   `image_demote` reverses the promotion.

## Undoing this

| Did | Undo with | Window |
|---|---|---|
| `instance_disk_attach` | `instance_disk_detach` | none stated |
| `image_promote` | `image_demote` | none stated |
| `disk_bulk_write_import_start` | `disk_bulk_write_import_stop` | none stated |
| `disk_delete` / `snapshot_delete` / `image_delete` | **nothing** | — |

## Errors

`{message, request_id, error_code}`. A `422` on `disk_create` is usually a quota or a size
constraint. A `400` on an attach usually means the instance is in a state that forbids it.
