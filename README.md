# Terraform Enterprise State Sync Workflow

This GitHub Actions workflow automatically synchronizes Terraform Enterprise (TFE) state files to an AWS S3 bucket. It can run on a schedule or be triggered manually. This is in case your current workflow is VCS based. You could otherwise perform a `terraform state pull` and use the output to sync it to the backup path you desire.

## Features

- Automated daily sync of Terraform state files
- Manual trigger option
- Secure handling of credentials
- Simple setup process

## Prerequisites

Before using this workflow, ensure you have:

1. A Terraform Enterprise account with:
   - Organization name
   - Workspace name
   - API token

2. AWS account with:
   - S3 bucket
   - IAM credentials with S3 write permissions

## Setup Instructions

1. Add the following secrets to your GitHub repository:
    * TFE_TOKEN # Your Terraform Enterprise API token
    * TFE_ORG # Your TFE organization name
    * TFE_WS # Your TFE workspace name
    * BUCKET_NAME # Your S3 bucket name
    * IAM_ROLE # AWS IAM role ARN


## Usage

### Automatic Execution
The workflow runs automatically at midnight (UTC) every day.

### Manual Execution
1. Go to the "Actions" tab in your repository
2. Select "Sync TFE State to S3" workflow
3. Click "Run workflow"

## Workflow Steps

1. Downloads the current state file from Terraform Enterprise
2. Configures AWS credentials
3. Uploads the state file to S3

## Security Considerations

- Use IAM roles with minimal required permissions
- Enable S3 bucket versioning
- Configure S3 bucket encryption
- Use secure TFE tokens with minimal scope
- Consider implementing IP restrictions

## Troubleshooting

Common issues:
- Ensure all required secrets are properly configured
- Verify AWS credentials have sufficient permissions
- Check TFE token has appropriate access rights
