# Submission setup

The four GitHub Actions workflows are already included under `.github/workflows/`.

The CI workflows need no AWS configuration. They can be run from GitHub Actions with **workflow_dispatch**.

The CD workflows intentionally do not contain credentials. Before running a CD workflow, configure these GitHub repository secrets:

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_REGION` (for the supplied Terraform setup, `us-east-1`)
- `EKS_CLUSTER_NAME` (the Terraform `cluster_name` output)
- `ECR_FRONTEND_REPO` (normally `frontend` for the supplied Terraform)
- `ECR_BACKEND_REPO` (normally `backend` for the supplied Terraform)
- `REACT_APP_MOVIE_API_URL` (the reachable URL of the deployed backend service, including `http://` or `https://` and without a trailing `/`)

Do not commit AWS credentials or real secret values into the repository.

The CD workflows tag images with `${{ github.sha }}` and use that same tag when applying the Kubernetes manifests, as required by the project specification.
