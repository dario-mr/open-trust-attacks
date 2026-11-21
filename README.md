# open-trust-attacks

A deliberately dishonest "vendor" for [Open Trust](https://github.com/dario-mr/open-trust): the same
demo app as [open-trust-demo](https://github.com/dario-mr/open-trust-demo), assessed in the ways a
vendor might try to get a certificate a buyer shouldn't accept. Each workflow run produces
certificates; `open-trust/demo/attacks/run.sh` verifies them as a strict buyer and records the result.

| Workflow job | What the vendor tries |
|---|---|
| `attacks.yml` / `assessor-current` | Control: the pinned Open Trust assessor, honestly |
| `attacks.yml` / `assessor-main` | The assessor at an unpinned ref (`@main`) |
| `attacks.yml` / `assessor-old` | An outdated assessor (v0.1.4) |
| `attacks.yml` / `own-pipeline` | Skip the isolated assessor: sign with the vendor's own job |
| `self-hosted.yml` / `own-self-hosted` | The vendor's own job on a vendor-controlled runner |
| `self-hosted.yml` / `hijack` | Route the isolated assessor's job onto a vendor runner labelled `ubuntu-24.04` |

Only `workflow_dispatch` triggers: the self-hosted runner is attached only while the test runs.
