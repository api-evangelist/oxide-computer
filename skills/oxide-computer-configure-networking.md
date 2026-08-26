---
name: oxide-configure-networking
description: Build VPCs, subnets, firewall rules and external addressing on an Oxide rack, and attach them to instances.
generated: '2026-08-26'
method: generated
source: openapi/oxide-computer-region-api-openapi.json
api: Oxide Region API
base_url: https://{oxide-control-plane-host}
operations:
  - vpc_list
  - vpc_create
  - vpc_view
  - vpc_delete
  - vpc_subnet_list
  - vpc_subnet_create
  - vpc_subnet_delete
  - vpc_firewall_rules_view
  - vpc_firewall_rules_update
  - vpc_router_list
  - vpc_router_create
  - vpc_router_route_create
  - instance_network_interface_create
  - instance_network_interface_delete
  - floating_ip_list
  - floating_ip_create
  - floating_ip_attach
  - floating_ip_detach
  - floating_ip_delete
  - instance_ephemeral_ip_attach
  - instance_ephemeral_ip_detach
  - external_subnet_create
  - external_subnet_attach
  - external_subnet_detach
  - internet_gateway_create
---

# Configure Oxide guest networking

## Vocabulary that catches people out

- **Floating IP** — persistent, re-attachable within a project. Survives the instance.
- **Ephemeral IP** — temporary, lifecycle-tied to the instance. Dies with it.
- **External subnet** — a routable subnet attached to instances, distinct from a VPC subnet.

Getting these three confused is the single most common Oxide networking mistake, and the API will
happily let you do the wrong one.

## Steps

1. **Create the VPC.** `vpc_create` (`POST /v1/vpcs?project=<project>`). Every project gets a
   default VPC, so check `vpc_list` first.
2. **Carve subnets.** `vpc_subnet_create` (`POST /v1/vpc-subnets?vpc=<vpc>&project=<project>`).
3. **Read the firewall before you write it.** `vpc_firewall_rules_view`
   (`GET /v1/vpc-firewall-rules?vpc=<vpc>`). Then `vpc_firewall_rules_update` — this is a
   **whole-collection PUT**, not a per-rule patch. Send the full desired rule set or you will
   delete rules you meant to keep. Read-modify-write, always.
4. **Attach an interface.** `instance_network_interface_create`
   (`POST /v1/network-interfaces?instance=<instance>`).
5. **Give it a public address.** `floating_ip_create` then `floating_ip_attach`
   (`POST /v1/floating-ips/{floating_ip}/attach`) for something durable;
   `instance_ephemeral_ip_attach` for something disposable.
6. **Route it.** `internet_gateway_create`, `vpc_router_create`, `vpc_router_route_create`.

## Undoing this

`floating_ip_detach`, `instance_ephemeral_ip_detach`, `external_subnet_detach` and
`instance_network_interface_delete` all cleanly reverse their attach. `vpc_delete`,
`vpc_subnet_delete` and `floating_ip_delete` are terminal. There is **no** transactional wrapper: a
multi-step network change that fails halfway leaves the earlier steps applied, and you must undo
them yourself in reverse order.

## Errors

`{message, request_id, error_code}`. `422` on a subnet create is usually a CIDR that overlaps an
existing subnet. `400` on an attach usually means the instance state forbids it.
