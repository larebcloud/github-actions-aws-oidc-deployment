Problem
Many GitHub → AWS setups still use long‑lived AWS access keys in GitHub, which is both insecure and difficult to rotate or manage. This increases the blast radius if GitHub secrets are ever leaked.

Solution
This project shows how to build a secure CI/CD pipeline that uses GitHub Actions to assume an AWS IAM role through OIDC, instead of relying on static access keys. The workflow gets short‑lived, automatically rotated credentials directly from AWS during each run.

Architecture
GitHub Actions workflows authenticate to AWS by assuming an IAM role via OIDC, and then use that role to deploy to an EC2 instance:

GitHub Actions → IAM Role (OIDC) → EC2

Key Security Features
No long‑lived AWS access keys are stored in GitHub; credentials are short‑lived and issued per workflow run.

The IAM role follows a least‑privilege model, granting only the permissions needed for the pipeline.

The role’s trust policy restricts access to a specific repository and branch, reducing the risk of unauthorized role assumption.

Verification
The workflow runs aws sts get-caller-identity to verify that it is using the correct IAM role and account during execution.

