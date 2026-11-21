# AWS DevOps Services


**Learning Program:** Codomax Digital Solutions  
**Topic:** AWS CodePipeline, CodeBuild, CodeDeploy, IAM, S3, and CloudWatch

---

## 1. Introduction to AWS DevOps

AWS provides services that support software development, automation, infrastructure management, monitoring, and application deployment.

These services help teams implement DevOps practices in cloud environments.

## 2. AWS CodePipeline

AWS CodePipeline is a managed continuous delivery service that automates software release workflows.

A pipeline can contain source, build, testing, approval, and deployment stages.

### Key Features

- Automated pipeline execution
- Integration with source repositories
- Multiple pipeline stages
- Integration with AWS build and deployment services
- Support for manual approval actions

### Example

GitHub → AWS CodePipeline → AWS CodeBuild → Deployment

## 3. AWS CodeBuild

AWS CodeBuild is a managed build service that can compile source code, run tests, and generate deployment artifacts.

### Key Features

- Managed build environments
- Automated build execution
- Support for multiple programming languages
- Integration with CodePipeline
- Build logs and execution status

### Example Build Process

1. Retrieve source code.
2. Install dependencies.
3. Execute tests.
4. Package application files.
5. Produce build artifacts.

CodeBuild can use a `buildspec.yml` file to define build commands.

## 4. AWS CodeDeploy

AWS CodeDeploy automates application deployments to supported compute environments.

It supports deployments to Amazon EC2, on-premises servers, AWS Lambda, and Amazon ECS.

### Key Benefits

- Automated deployment processes
- Deployment status tracking
- Support for different deployment strategies
- Reduced manual deployment steps
- Integration with other AWS DevOps services

## 5. Amazon S3 in CI/CD

Amazon Simple Storage Service (S3) is an object storage service.

In DevOps, S3 can be used for:

- Storing build artifacts
- Hosting static websites
- Storing deployment packages
- Managing application assets

### Example

A GitHub Actions workflow uploads HTML and CSS files to an S3 bucket after successful validation.

## 6. AWS IAM

AWS Identity and Access Management (IAM) controls access to AWS services and resources.

### Important Concepts

- IAM users
- IAM groups
- IAM roles
- IAM policies
- Least-privilege permissions

### IAM in CI/CD

A deployment pipeline needs permission to access its deployment destination.

For example, a GitHub Actions workflow can assume an IAM role with permission to upload files to a specific S3 bucket.

## 7. OpenID Connect (OIDC)

OpenID Connect allows an external identity provider, such as GitHub Actions, to exchange an identity token for temporary AWS credentials through AWS Security Token Service (STS).

### Authentication Flow

GitHub Actions → OIDC Token → AWS STS → Temporary Credentials → Authorized AWS Resources

### Advantages

- Avoids storing long-term AWS access keys.
- Uses temporary credentials.
- Supports repository and branch restrictions.
- Helps implement least-privilege access.

## 8. Amazon CloudWatch

Amazon CloudWatch is an AWS monitoring and observability service.

It helps collect and analyze metrics, logs, and alarms.

### Uses in DevOps

- Monitoring application performance
- Reviewing service logs
- Creating operational alerts
- Tracking failures
- Investigating deployment-related issues

## 9. GitHub Actions vs. AWS CodePipeline

| Feature | GitHub Actions | AWS CodePipeline |
|---|---|---|
| Provider | GitHub | AWS |
| Workflow definition | YAML workflows | AWS pipeline configuration |
| Main purpose | General repository automation and CI/CD | Managed release pipeline orchestration |
| GitHub integration | Native | Supported through source integrations |
| AWS deployment | Through credentials and AWS integrations | Through AWS deployment integrations |

Both can be used in AWS-based CI/CD solutions.

## 10. Example AWS CI/CD Architecture

A typical pipeline can follow this design:

1. Source code is stored in GitHub.
2. A change triggers the pipeline.
3. CodeBuild builds and tests the application.
4. CodePipeline coordinates the workflow.
5. CodeDeploy deploys the application to a supported compute platform.
6. CloudWatch provides monitoring information.

For static websites, deployment can be simplified by uploading files directly to S3.

## 11. Security Best Practices

- Apply least-privilege IAM permissions.
- Use temporary credentials where possible.
- Restrict access to deployment environments.
- Protect sensitive configuration values.
- Review deployment logs.
- Enable appropriate monitoring.
- Avoid exposing private S3 objects.

## 12. Key Learnings

I learned how AWS services support the different stages of software delivery.

I also understood the roles of CodePipeline, CodeBuild, CodeDeploy, S3, IAM, OIDC, and CloudWatch in CI/CD architecture.

## 13. Conclusion

AWS DevOps services provide tools for automating software integration, testing, deployment, and monitoring.

Understanding these services helps in designing secure, repeatable, and scalable cloud delivery workflows.

## References

- AWS CodePipeline: https://docs.aws.amazon.com/codepipeline/
- AWS CodeBuild: https://docs.aws.amazon.com/codebuild/
- AWS CodeDeploy: https://docs.aws.amazon.com/codedeploy/
- AWS IAM: https://docs.aws.amazon.com/iam/
- Amazon CloudWatch: https://docs.aws.amazon.com/cloudwatch/
