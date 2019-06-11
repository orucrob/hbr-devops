# hbr-devops

This is an example of CI/CD in pure AWS.
Take a look into `buildspec.yaml` and `template_devops.yaml`.

Other files are just SAM example.

## template_devops.yaml

This file contains full IaC for CI/CD infrastructure.

## buildspec.yaml

Build file for CodeBuild - it packages sam application.

# Deployment of CI/CD infrastructure

Packaging:

```
aws cloudformation package --template-file .\template_devops.yaml --output-template-file packaged_devops.yaml --s3-bucket <<e.g. devops-bucket>>

```

Deploying:

```
aws cloudformation deploy --template-file  .\packaged_devops.yaml --stack-name hbr-devops-cicd --capabilities CAPABILITY_IAM CAPABILITY_NAMED_IAM --parameter-overrides Env=dev
```

-   **--stack-name** - can be used whatever you want
-   **Env** parameter - needs to be the same as branch in repo (default: dev)
-   **Repo** parameter - codecommit repo in this account and this region with module source files (default: hbr-devops)
-   **ArtifactBucket** parameter - Devops S3 bucket for storing artifacts from build (default: devops-bucket)
