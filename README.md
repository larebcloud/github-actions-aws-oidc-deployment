# Secure GitHub Actions → AWS EC2 Deployment using IAM OIDC

## Problem
Many GitHub → AWS setups rely on long-lived AWS access keys stored as GitHub secrets,
which increases security risk and operational overhead.

## Solution
This project demonstrates a secure CI/CD pipeline using GitHub Actions
with AWS IAM OIDC authentication, eliminating static credentials.

## Architecture
GitHub Actions → IAM Role (OIDC) → EC2

## Key Security Features
- No long-lived AWS access keys stored in GitHub
- Short-lived credentials issued per workflow run
- Least-privilege IAM role
- Trust policy restricted to repo + branch

## Verification
The workflow uses `aws sts get-caller-identity`
to confirm successful role assumption.

## Common Issues & Fixes
- AccessDenied → trust policy mismatch
- Workflow not triggering → branch condition mismatch
- No permissions → missing IAM actions
