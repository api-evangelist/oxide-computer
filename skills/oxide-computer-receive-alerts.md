---
name: oxide-receive-alerts
description: Stand up a webhook receiver on an Oxide rack, subscribe it to alert classes, verify the HMAC signature, and test delivery.
generated: '2026-08-26'
method: generated
source: openapi/oxide-computer-region-api-openapi.json + https://docs.oxide.computer/guides/alerts/webhooks
api: Oxide Region API
base_url: https://{oxide-control-plane-host}
operations:
  - alert_class_list
  - webhook_receiver_create
  - webhook_receiver_update
  - alert_receiver_list
  - alert_receiver_view
  - alert_receiver_delete
  - alert_receiver_probe
  - alert_receiver_subscription_add
  - alert_receiver_subscription_remove
  - alert_list
  - alert_view
  - alert_delivery_list
  - alert_delivery_resend
  - webhook_secrets_list
  - webhook_secrets_add
  - webhook_secrets_delete
---

# Receive Oxide alerts over webhooks

Alerts are how the rack talks back. The REST API lets you make requests of the rack; alerts let the
rack notify you when something happens — an SSD fault, an instance reboot.

**You need `fleet.admin`.** Alert receivers may only be created or modified by fleet admins.

## Steps

1. **Discover the classes.** `alert_class_list` (`GET /v1/alert-classes`). Do this against the
   actual rack — Oxide does not publish the class registry as static documentation, and the
   examples in its docs (`hardware.turboencabulator.fault.side_fumbling_detected`) are deliberately
   imaginary.
2. **Create the receiver.** `webhook_receiver_create` (`POST /v1/webhook-receivers`) with your
   HTTPS endpoint and initial subscriptions.
3. **Subscribe more classes.** `alert_receiver_subscription_add`
   (`POST /v1/alert-receivers/{receiver}/subscriptions`). Subscriptions support per-segment globs:
   `*` matches one segment, `**` matches any number. A segment is either literal text or a glob —
   `example.*_thingy.some_event` is rejected.
4. **Verify signatures on every delivery.** Each POST carries
   `x-oxide-signature: a=sha256&id={secret-id}&s={signature}`, hex-encoded HMAC-SHA256. When the
   receiver has several secrets you get several headers — accept a delivery if **any** verifies.
   That is how rotation works: `webhook_secrets_add` the new one, wait, `webhook_secrets_delete`
   the old one.
5. **Test it.** `alert_receiver_probe` (`POST /v1/alert-receivers/{receiver}/probe`) sends a
   synthetic alert with `delivery.trigger = "probe"`. Use this instead of waiting for a real fault.
6. **Handle the payload.** `{alert_class, alert_id, data:{version,...}, delivery:{id, receiver_id,
   sent_at, trigger}}`. The `data` schema is class-specific and carries its own `version` — branch
   on `alert_class` first, then on `data.version`.

## Delivery guarantees you must design around

- Success requires a **2xx**. Anything else — including a 3xx — is a failure.
- The timeout is **30 seconds**. Acknowledge fast, process asynchronously.
- Failures are retried **up to two times**. That is it. Design for loss.
- Backfill with `alert_delivery_list` (`GET /v1/alert-receivers/{receiver}/deliveries`) and pull
  missed events with `alert_view`; `alert_delivery_resend`
  (`POST /v1/alerts/{alert_id}/resend`) re-sends a specific alert.
- `alert_delivery_resend` is **not** a reversal — it re-sends something that already fired.

## Undoing this

`alert_receiver_subscription_remove` reverses a subscription add.
`alert_receiver_delete` removes the receiver entirely; there is no restore.
