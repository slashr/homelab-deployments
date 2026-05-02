# kash

Kubernetes manifests for the read-only dashboard and paper-first Kalshi research
jobs.

## Paper Watchdog

`paper-watchdog-cronjob.yaml` is the intended always-on paper collection job.
It runs one paper collection cycle every 30 minutes.

On images that include `paper-watchdog`, it records paper observations, bounded
rejection diagnostics, paper outcomes, and CLV snapshots into the shared
`kash-data` SQLite volume. Diagnostic rejections are for Paper Ops visibility and
do not count as readiness evidence. On older images, it falls back to
`evaluate-watchlist --save` plus `clv-watchlist --save` so evidence collection
can start before the next kash image rollout. It does not pass `--execute`, and
neither path exposes an order-execution switch.

The CronJob intentionally matches the current evidence lane:

- strategy: `watchlist_source_edge_v1`
- experiment: `watchlist-edge-001`
- source types: `sportsbook_no_vig,sportsbook_position_total`
- entry range: `0.40` through `0.499999`
- aggregate target: at least `55%` settled paper win rate
- readiness sample floor: at least `20` settled current-policy candidates

The previous `kash-auto-runner` Deployment has been removed from GitOps. Argo CD
prune should delete that workload from the cluster if it exists; it used the
removed `auto-operate` command and is not part of the paper-first strategy.

## Secrets

Credentials are supplied by the SOPS-encrypted `kash-secrets` Secret. Do not add
plaintext API keys or private key material to this repository.
