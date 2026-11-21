# CI/CD Deployment Workflow Documentation


**Learning Program:** Codomax Digital Solutions  
**Project:** GitHub Actions to Amazon S3 Deployment Pipeline

---

## 1. Project Overview

This document explains the architecture, configuration, and workflow of a basic CI/CD pipeline designed to deploy a static website from GitHub to Amazon S3.

The purpose of this exercise is to understand how source control, automated validation, AWS authentication, and cloud deployment work together.

The pipeline was explored as a practical learning activity. An IAM OIDC authorization error was encountered during execution, so a successful deployment has not yet been verified.

## 2. Project Objectives

- Understand the deployment pipeline lifecycle.
- Explore GitHub Actions automation.
- Learn how GitHub workflows connect to AWS.
- Understand IAM roles and OIDC authentication.
- Document the deployment process.
- Identify and troubleshoot common CI/CD errors.

## 3. Tools and Technologies

| Technology | Purpose |
|---|---|
| Git | Version control |
| GitHub | Source-code hosting |
| GitHub Actions | Workflow automation |
| AWS IAM | Authentication and authorization |
| AWS STS | Temporary AWS credentials |
| Amazon S3 | Static website deployment destination |
| YAML | Workflow configuration |
| HTML | Example website content |

## 4. Proposed Architecture

Developer → GitHub Repository → GitHub Actions → AWS IAM/OIDC → Amazon S3 → Live Website

### Architecture Explanation

1. A developer updates the website source code.
2. Git tracks the changes.
3. The changes are pushed to GitHub.
4. GitHub Actions starts the workflow.
5. The workflow validates the required website files.
6. GitHub requests temporary AWS credentials through OIDC.
7. AWS evaluates the IAM role's trust policy.
8. If authorization succeeds, GitHub Actions uploads website files to Amazon S3.
9. The deployed website can be accessed through its configured hosting endpoint.

## 5. Repository Structure

```text
aws-devops-cicd-pipeline/
├── .github/
│   └── workflows/
│       └── deploy-s3.yml
├── website/
│   └── index.html
└── README.md
```

## 6. GitHub Actions Workflow

The workflow file is stored at:

`.github/workflows/deploy-s3.yml`

### Workflow Trigger

The pipeline is configured to start when changes are pushed to the `main` branch.

It also supports manual execution using `workflow_dispatch`.

### Workflow Stages

**Checkout Repository**

Downloads the repository content into the GitHub Actions runner.

**Validate Website**

Checks whether the expected HTML file exists and contains basic HTML tags.

**Configure AWS Credentials**

Requests temporary AWS credentials by assuming an IAM role through GitHub OIDC.

**Deploy Website to S3**

Uses the AWS CLI to synchronize selected website files with the S3 bucket.

## 7. AWS Authentication

The proposed pipeline uses an IAM role named:

`GitHubActionsS3DeployRole`

The role is intended to trust GitHub Actions requests from the authorized repository and branch.

The IAM permissions policy is designed to allow listing the deployment bucket and uploading website files.

### Why OIDC Is Used

OIDC avoids storing permanent AWS access keys in the GitHub repository.

AWS Security Token Service validates the identity token and issues temporary credentials when the IAM trust conditions are satisfied.

## 8. Deployment Command

The AWS CLI can upload website files using:


This command synchronizes files from the local `website/` directory to the target S3 bucket.

For a deployment pipeline, additional include/exclude rules can limit which file types are uploaded.

## 9. Testing Procedure

The intended verification process is:

1. Push a website change to `main`.
2. Open the GitHub Actions tab.
3. Inspect the workflow run.
4. Confirm that validation succeeds.
5. Confirm that AWS authentication succeeds.
6. Confirm that S3 upload succeeds.
7. Open the live website.
8. Verify that the updated content appears.

## 10. Issue Encountered

During workflow execution, the following error occurred:

`Could not assume role with OIDC: Not authorized to perform sts:AssumeRoleWithWebIdentity`

### Meaning

AWS rejected the attempt to assume the deployment IAM role using the GitHub OIDC token.

### Potential Causes

- Incorrect IAM trust policy
- Mismatch in repository or branch restrictions
- Incorrect OIDC audience
- Incorrect identity-provider configuration
- Mismatch between token claims and trust conditions

### Troubleshooting Approach

1. Verify the IAM role ARN.
2. Inspect the role's trust relationship.
3. Confirm the GitHub OIDC provider exists.
4. Check the expected token audience.
5. Compare the GitHub OIDC subject with the IAM trust conditions.
6. Retry the workflow after correcting the configuration.

## 11. Security Considerations

- Use least-privilege IAM permissions.
- Restrict role assumption to authorized workflows.
- Avoid permanent access keys.
- Protect the main branch.
- Do not expose sensitive configuration in logs.
- Keep deployment permissions limited to the intended resources.

## 12. Lessons Learned

This exercise helped me understand that CI/CD requires both workflow automation and secure authentication.

I learned that even when a workflow is configured correctly, deployment can fail if the IAM trust policy does not match the identity presented by GitHub.

Troubleshooting authentication is an important part of maintaining secure deployment pipelines.

## 13. Conclusion

This document describes the design and attempted configuration of a GitHub Actions pipeline for Amazon S3 deployment.

Although successful deployment was not verified, the exercise provided practical learning about workflow configuration, IAM roles, OIDC authentication, deployment commands, and CI/CD troubleshooting.

## References

- GitHub Actions: https://docs.github.com/en/actions
- GitHub OIDC with AWS: https://docs.github.com/en/actions/how-tos/secure-your-work/security-harden-deployments/oidc-in-aws
- AWS IAM: https://docs.aws.amazon.com/iam/
- Amazon S3: https://docs.aws.amazon.com/s3/
