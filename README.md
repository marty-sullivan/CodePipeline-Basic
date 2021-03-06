# CodePipeline Template

This repository is a template for applications deployed with CodePipeline -> CodeBuild -> CloudFormation



### GitHub Authentication Setup (Currently Manual)

1. Create a Personal Access Token in GitHub for CodePipeline: https://docs.aws.amazon.com/codepipeline/latest/userguide/GitHub-create-personal-token-CLI.html
2. Place the Personal Access Token in an SSM Parameter in the desired AWS Account / Region named `/CodePipeline/GitHub`

### Initial Deployment

1. Authenticate to desired AWS Account with Administrator Access in your bash shell
2. Navigate to root directory of this repository
4. Run `./init`
5. Watch CloudFormation console for progress deploying initial stack (`build/template.yml`)
6. Watch CodePipeline console for progress of first pipeline run & monitor CodeBuild + CloudFormation progress
7. Commit + Push changes to branch in order to trigger a new build

### Application Destruction (Currently Manual)

1. Delete any objects from S3 Buckets (Build + Web + Web Logs)
2. Delete any ECR Container Images
3. Delete any Manual Route53 Records (e.g. ACM cert verification CNAMEs)
4. Delete the CloudFormation Stack for the deployment

### Notes

* CodeBuild + CodePipeline + CloudFormation IAM Roles are currently overprivileged and should be scoped better 
* Load Balancer should be configured to make a better HA ECS deployment
* Web Stack is currently disabled (commented out) but will enable CloudFront + API Gateway + Lambda (talk to Marty first if you want to explore)
* Load Balancer could be added as an origin behind CloudFront + Route53 Config
