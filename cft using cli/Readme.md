# Using CLI

## steps for the vpc & security Group Setup in multi regions

1. To launch the template using AWS CloudFormation (CFT) from the CLI, you can use the aws cloudformation create-stack command. First, save the template content to a file, for example, vpc-security-template.yaml. Then, you can use the following command:

    ```console
    aws cloudformation create-stack --stack-name my-vpc-stack --template-body file://vpc-security-template.yaml
    ```

    Make sure to replace my-vpc-stack with the desired name for your CloudFormation stack, and vpc-security-template.yaml with the actual path to your template file.

    This command will create a CloudFormation stack with the specified name and use the template file to provision the resources defined in the template.

    To specify the region when launching the CloudFormation stack, you can include the --region parameter in the aws cloudformation create-stack command. 

    ```console
    aws cloudformation create-stack --stack-name my-vpc-stack --template-body file://vpc-security-template.yaml --region us-west-2
    ```

2. After executing the Above command, CloudFormation will initiate the stack creation process. You can monitor the stack creation progress by using the aws cloudformation describe-stacks command:

    ```console
    aws cloudformation describe-stacks --stack-name my-vpc-stack
    ```

3. This command will provide information about the stack, including its current status. Once the stack creation is complete, you can obtain the output values (VPC ID, Internet Gateway ID, Subnet ID, Route Table ID, Security Group ID) using the aws cloudformation describe-stacks command with the --query option:

    ```console
    aws cloudformation describe-stacks --stack-name my-vpc-stack --query 'Stacks[0].Outputs'
    ```

    Replace my-vpc-stack with the name of your CloudFormation stack. The command will return the output values specified in your CloudFormation template.

    > Note: Ensure that you have the AWS CLI installed and configured with your access key and secret access key before running these commands.

4. To check the CloudFormation stacks that are currently present in your AWS account, you can use the aws cloudformation list-stacks command. Here's an example:

    ```console
    aws cloudformation list-stacks
    ```

5. To stop or delete CloudFormation stacks, you can use the aws cloudformation delete-stack command.

    ```console
    aws cloudformation delete-stack --stack-name STACK_NAME
    ```

## steps for the ec2 template

1. Use the create-stack command with the AWS CLI to create the stack. 

    ```console
    aws cloudformation create-stack --stack-name ec2-stack --template-body file://ec2-stack.yaml --parameters ParameterKey=InstanceType,ParameterValue=t2.micro --region us-west-2
    ```

2. Wait for the stack creation to complete. You can use the describe-stacks command to check the status of the stack creation:

    ```console
    aws cloudformation describe-stacks --stack-name ec2-stack --region us-west-2
    ```

3. To delete the CloudFormation stack, you can use the delete-stack command with the AWS CLI.

    ```console
    aws cloudformation delete-stack --stack-name ec2-stack --region us-west-2
    ```