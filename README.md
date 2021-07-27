# AWS-CDK-S3-bucket-deployment
This repository describes the steps I took in using AWS CDK for the creation of a stack which contains an S3 bucket. 

**Step 1** - Initialise a new project by running the following command. For this project, I will be using Python.

```sh
cdk init app --language python
```

Open a virtual environment and install the necessary requirements using pip.

```sh
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

Then, install the module that manages S3.

```sh
pip install aws-cdk.aws-s3
```

**Step 2** - Open the project directory defined as <project_name>, and edit the file named <project_name_stack.py>. In my example, I called the project ApplicationStack and the generated Python file received the name application_stack_stack.py. The code that I added to the Python file is the following:

```python
from aws_cdk import core as cdk
from aws_cdk import aws_s3 as s3

class ApplicationStackStack(cdk.Stack):

    def __init__(self, scope: cdk.Construct, construct_id: str, **kwargs) -> None:
        super().__init__(scope, construct_id, **kwargs)
        bucket = s3.Bucket(self, "carmenilie-s3-bucket-with-cdk")
```

**Step 3** *(Optional)* - Preview the CloudFormation template using the next command:

```sh
cdk synth
```

**Step 4** - Deploy the application with the command below:

```sh
cdk deploy --all
```

The output should be similar to the following one:

```sh
ApplicationStackStack: deploying...
ApplicationStackStack: creating CloudFormation changeset...
  0/3 |4:46:12 PM | REVIEW_IN_PROGRESS   | AWS::CloudFormation::Stack | ApplicationStackStack User Initiated
  0/3 |4:46:17 PM | CREATE_IN_PROGRESS   | AWS::CloudFormation::Stack | ApplicationStackStack User Initiated
  0/3 |4:46:21 PM | CREATE_IN_PROGRESS   | AWS::S3::Bucket    | carmenilie-s3-bucket-with-cdk (carmenilies3bucketwithcdkCD85824B)
  0/3 |4:46:21 PM | CREATE_IN_PROGRESS   | AWS::CDK::Metadata | CDKMetadata/Default (CDKMetadata)
  0/3 |4:46:22 PM | CREATE_IN_PROGRESS   | AWS::S3::Bucket    | carmenilie-s3-bucket-with-cdk (carmenilies3bucketwithcdkCD85824B) Resource creation Initiated
  0/3 |4:46:23 PM | CREATE_IN_PROGRESS   | AWS::CDK::Metadata | CDKMetadata/Default (CDKMetadata) Resource creation Initiated
  1/3 |4:46:23 PM | CREATE_COMPLETE      | AWS::CDK::Metadata | CDKMetadata/Default (CDKMetadata)
  2/3 |4:46:43 PM | CREATE_COMPLETE      | AWS::S3::Bucket    | carmenilie-s3-bucket-with-cdk (carmenilies3bucketwithcdkCD85824B)
  3/3 |4:46:44 PM | CREATE_COMPLETE      | AWS::CloudFormation::Stack | ApplicationStackStack

 ✅  ApplicationStackStack
```

In the end, open the AWS Console and check the creation of the CloudFormation stack and of the bucket.
