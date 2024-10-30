# Challenge description:

    Create an S3 bucket in Versent innovation-shared account with the standard security attributes (encryption at rest, encryption at transfer, private access, etc).

    Using GitHub Workflow Actions, create workflow that will push your code to an S3 bucket in Versent innovation-shared account to a specific S3 path (e.g. s3://mybucket-abc123/haris/challenge2.zip).

    Create a CodePipeline pipeline with the following general specifications:

        Source is the zip file you pushed to the S3 bucket.

        It will have three parameters: dev_env, uat_env, prod_env.

        The pipeline will use the combination of the zip file and the parameters to run three stages, each will deploy an SSM parameter with different name, which represents CI/CD stages deployment to different environments, e.g. dev, uat, and prod.

        The name of the SSM parameters  should follow this pattern:
        /<prefix of your choice>/dev
        /<prefix of your choice>/uat
        /<prefix of your choice>/prod
        With the value from dev_env pipeline parameter will be stored in /<prefix of your choice>/dev SSM parameter, and so on.

        The stages for the CodePipeline pipeline will look like:
        Source → Deploy to Dev → Deploy to UAT → Deploy to Prod
        Deploy to Dev will only deploy the SSM Parameter /<prefix of your choice>/dev
        Deploy to UAT will only deploy the SSM Parameter /<prefix of your choice>/uat
        Deploy to Prod will only deploy the SSM Parameter /<prefix of your choice>/prod

    Create another GitHub Workflow Actions that can capture the input from user as variables dev_input, uat_input, prod_input , and start the CodePipeline pipeline from the previous step passing these variables for the pipeline variables, with value from dev_input will be used for dev_env, uat_input will be used for uat_env, prod_input will be used for prod_env.

    To create/update the SSM parameter from your CodePipeline you can use any tools that you can think of. CloudFormation with AWS CLI, CloudFormation with sceptre, CloudFormation with CodePipeline deploy action, Terraform, Ansible, or even AWS CLI for SSM. Just make sure if we run it multiple times it will not crash, and the SSM parameters will have the expected value.

    Ensure others can run your GitHub Workflow Actions.
