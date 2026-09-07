# box-watch: retired scheduled watcher

Retired on 2026-09-07. GitHub's nominal 10-minute schedule ran hours apart,
causing the 30-minute Kuma heartbeat to alternate Down/Up while the server
and applications were healthy. The workflow is disabled and has no cron,
heartbeat or email step. Its remaining code is an optional manual diagnostic.

Production monitoring:

- Cloudflare Tunnel Health policy `box-sg tunnel health` watches the Singapore
  tunnel externally, including when the host is powered off or disconnected.
- Uptime Kuma checks applications every 60 seconds, with two retries before
  alerting. Protected status/Kuma applications are checked through internal
  Caddy routing with expected page content and redirects disabled; the
  Cloudflare Access login page cannot stand in for a working application.
- The old GitHub heartbeat monitor #10 is paused with notifications detached.
  Its history is retained, not relabeled as server downtime.

Limits: tunnel health describes connectivity, not host power. A stopped app
can leave the tunnel healthy; the application monitors cover that case.
Cloudflare remains a shared dependency for ingress and the external alarm.
No independent third-party uptime service was provisioned.
