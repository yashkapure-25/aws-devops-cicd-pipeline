# AWS DevOps & CI/CD

**Learning Program:** Codomax Digital Solutions  
**Topic:** Git, GitHub, Version Control, Continuous Integration, Continuous Deployment, and AWS DevOps

## Project Overview

This repository documents my learning journey through AWS DevOps and CI/CD fundamentals.

The module focuses on understanding version control, automated integration, deployment pipelines, and AWS services used in modern DevOps workflows.

## Learning Objectives

- Understand Git and GitHub fundamentals.
- Learn version control and branching.
- Understand Continuous Integration (CI).
- Understand Continuous Delivery and Continuous Deployment (CD).
- Explore AWS CI/CD services.
- Study the architecture and stages of a basic deployment pipeline.
- Document the deployment workflow.

## Technologies and Tools Studied

- Git
- GitHub
- GitHub Actions
- AWS IAM
- Amazon S3
- AWS CodePipeline
- AWS CodeBuild
- AWS CodeDeploy

## What Is DevOps?

DevOps combines software development and IT operations practices to improve collaboration, automation, software quality, and delivery speed.

Its key practices include version control, continuous integration, automated testing, continuous delivery, monitoring, and feedback.

## What Is CI/CD?

**Continuous Integration (CI)** involves frequently merging code changes and automatically running validation or tests.

**Continuous Delivery** keeps validated changes ready for release, typically with a manual approval or release step.

**Continuous Deployment** automatically releases changes that pass the pipeline's required checks.

## Example CI/CD Architecture

Developer → GitHub Repository → GitHub Actions → Validation → AWS S3 → Website

This is a reference architecture for deploying a static website.

## Deployment Workflow

1. A developer updates the website source code.
2. Git tracks the changes.
3. The changes are committed and pushed to GitHub.
4. A GitHub Actions workflow starts.
5. The pipeline validates the website files.
6. The workflow authenticates to AWS using IAM and OIDC.
7. If authorized, the pipeline uploads the website files to Amazon S3.
8. The deployed website can be tested using its hosting endpoint.

## AWS CI/CD Services

| Service | Purpose |
|---|---|
| AWS CodePipeline | Orchestrates pipeline stages |
| AWS CodeBuild | Builds and tests applications |
| AWS CodeDeploy | Automates application deployments |
| Amazon S3 | Stores artifacts and static website files |
| AWS IAM | Controls access to AWS resources |
| Amazon CloudWatch | Provides logs, metrics, and monitoring |

## Security Best Practices

- Use least-privilege IAM permissions.
- Prefer temporary credentials and OIDC over permanent access keys.
- Protect the main branch.
- Never commit passwords, tokens, or AWS access keys.
- Review workflow permissions and deployment logs.

## Practical Exploration

I explored a GitHub Actions deployment workflow designed to upload static website files to Amazon S3.

During configuration, I encountered an AWS OIDC role-assumption authorization error. This highlighted the importance of IAM trust policies, identity-provider configuration, and secure CI/CD authentication.

The deployment pipeline is documented as a learning exercise rather than a verified successful deployment.

## Key Learnings

- Git maintains a history of source-code changes.
- GitHub supports collaboration and repository management.
- CI/CD reduces repetitive integration and deployment work.
- AWS provides managed services for build and deployment automation.
- IAM and OIDC are important for secure pipeline authentication.
- Deployment workflows should include validation, logging, and error handling.

## Conclusion

This module helped me understand Git, GitHub, version control, CI/CD automation, AWS DevOps services, and deployment pipeline architecture.

**Learning Program:** Codomax Digital Solutions
