# box-watch

Off-box liveness check for box-sg (BEV-5 P4-M4). GitHub's scheduler probes `keywars.io/api/health` and
`status.shuf.dev` every 10 minutes and emails via Resend when both retries fail. Secrets: `RESEND_KEY`,
`ALERT_FROM`, `ALERT_TO` (repository secrets, set from the box's `alert.env`, never committed).

Force a test: Actions → box-watch → Run workflow → `target` = `https://does-not-exist.shuf.dev/`.
Monthly keepalive commit keeps the schedule enabled (GitHub disables schedules after 60 days without commits).
