# Rubric map

Implemented in this package:

- `.github/workflows/frontend-ci.yaml` — frontend PR/manual CI; parallel lint and test; Docker build gated by both.
- `.github/workflows/backend-ci.yaml` — backend PR/manual CI; parallel lint and test; Docker build gated by both.
- `.github/workflows/frontend-cd.yaml` — frontend main/manual CD; lint/test; SHA-tagged ECR image; EKS deployment with the same SHA.
- `.github/workflows/backend-cd.yaml` — backend main/manual CD; lint/test; SHA-tagged ECR image; EKS deployment with the same SHA.
- Kubernetes manifests are retained and are updated at deployment time with Kustomize, so committed manifests are not polluted by generated image tags.
- Frontend lint configuration was simplified to use the declared ESLint/React tooling without an undeclared Prettier parser dependency.
- Backend Docker installation uses `pipenv install --system --skip-lock` to avoid requiring a stale lock resolution during image construction.

Not embedded intentionally:

- AWS access keys, ECR URLs, EKS cluster names, and deployed backend URLs. These are environment/account-specific and must never be fabricated or committed into source control.

See `SUBMISSION_SETUP.md` for the exact GitHub secret names required by the CD workflows.
