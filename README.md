# Homelab Deployments

Declarative Kubernetes manifests for the services that run my homelab. Each
service lives under `src/` while the GitOps automation that keeps the cluster in
sync lives under `argo/`. Temporary or experimental manifests are kept under
`temp/` until they are ready to graduate into `src/`.

## Repository layout

### `src/`

Application-specific manifests. Notable subdirectories include:

- `adguard` – DNS and filtering deployment (ConfigMap, Deployment, PVC,
  Service, Ingress).
- `dream-home-bot` – Stateful bot workload.
- `homelab-map` – Aggregator, agent, frontend, namespace, and ingress for the
  map UI.
- `mediaserver` – Media services (for example Plex) manifests.

### `argo/`

Argo CD `Application` definitions and release pipelines that continuously apply
the manifests from `src/`. Each subfolder mirrors a service (for example
`argo/homelab-map/release.yaml` syncs the map workloads).

### `temp/`

Scratch space for manifests that are still being validated (for example new Plex
or Grafana deployments). Nothing here is production-ready until it is promoted
into `src/` and `argo/`.

### Supporting files

- `.github/` – CI workflows.
- `AGENTS.md` – Describes the FAW (Fully Automated Workflow) policy.
- `TASKS.md` – Source of truth for FAW work tracking (tasks, status, acceptance).
- `PLAN.md` – Working notes for the in-flight FAW task.

## Working in FAW mode

1. Read `AGENTS.md` for the full FAW loop.
2. Claim the first task marked `FAW: on` and `Status: TODO` inside `TASKS.md`,
   update it to `IN_PROGRESS`, and capture the plan in `PLAN.md`.
3. Follow the FAW checklist end-to-end (branch, commits, PR, checks,
   review/👍, merge, release watch, task closure).

Keeping these documents current ensures that anyone jumping into the repo
understands what is running in the homelab and what automation is expected.
