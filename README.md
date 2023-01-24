# my_terraform_series_notes

## **Introduction to Terraform**

Key Concepts:
a) **Infrastructure as a Code**
  - Managing and provisioning of infrastructure through code instead of manually
  - Files that contain configurations are created and makes it easy to edit and distribute
  - Ensures that the same environment is provisioned everytime.
  - Helps avoid undocumented, ad-hoc configuration changes
  - Easy to version control
  - Can create infrastructure in modular components
  - Gives you a template to follow for provisioning
b) **Benefits:**
  - Cost reduction
  - Increase in speed of deployment
  - Reduce errors
  - Improve infrastructure consistency
  - Eliminate configuration drift

##**What is Terraform?:**
  - IaaC tool from Hashicorp
  - Used for building, changing and managing infrastructure in a safe, repeatable way
  - Uses HCL - Hashicorp Configuration Language - human readable
  - Reads configuration files and provides an execution plan which can be reviewed before being applied.
  - It is platform agnostic - can manage a heterogeneous environment - multi cloud
  - State management - creates a state file when a project is first initialized. Uses this state file to  create plans and make changes based on the desired and current state of the infrastructure.
  - Creates operator confidence

  ##**Terraform Configuration Files**
- Terraform uses declarative syntax to describe your Infrastructure as Code (IaC) infrastructure
and then persist it in configuration files that can be shared, reviewed, edited, versioned,
preserved, and reused.
- Terraform configuration files can use either of two formats: Terraform domain-specific
language (HashiCorpConfiguration Language format [HCL]), which is the recommended
approach, or JSON format if the files need to be machine-readable.
- Configuration files that use the HCL format end with the .tf file extension;
- Those using JSON format end with the .tf.json file extension.
- The Terraform format is human-readable, while the JSON format is machine readable


# Terraform & AWS CLI Installation

## A) Prerequisites
- Install Terraform CLI
- Install AWS CLI
- Install VS Code Editor - recommended for this course
- Install HashiCorp Terraform plugin for VS Code - recommended


## B) MACOS - Terraform Install
- [Download Terraform MAC](https://www.terraform.io/downloads.html)
- [Install CLI](https://learn.hashicorp.com/tutorials/terraform/install-cli)
- Unzip the package
```
# Copy binary zip file to a folder
mkdir /Users/<YOUR-USER>/Documents/terraform-install
COPY Package to "terraform-install" folder

# Unzip
unzip <PACKAGE-NAME>
unzip terraform_1.0.10_darwin_amd64.zip

# Copy terraform binary to /usr/local/bin
echo $PATH
mv terraform /usr/local/bin

# Verify Version
terraform version

# To Uninstall Terraform (NOT REQUIRED)
rm -rf /usr/local/bin/terraform
```

## C) MACOS - Install VSCode Editor and terraform plugin
- [Microsoft Visual Studio Code Editor](https://code.visualstudio.com/download)
- [Hashicorp Terraform Plugin for VS Code](https://marketplace.visualstudio.com/items?itemName=HashiCorp.terraform)


### D) MACOS - Install AWS CLI
- [AWS CLI Install](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)
- [Install AWS CLI - MAC](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-mac.html#cliv2-mac-install-cmd)

```
# Install AWS CLI V2
curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /
which aws
aws --version

# Uninstall AWS CLI V2 (NOT REQUIRED)
which aws
ls -l /usr/local/bin/aws
sudo rm /usr/local/bin/aws
sudo rm /usr/local/bin/aws_completer
sudo rm -rf /usr/local/aws-cli
```


## E) MACOS - Configure AWS Credentials
- **Pre-requisite:** Should have AWS Account.
  - [Create an AWS Account](https://portal.aws.amazon.com/billing/signup?nc2=h_ct&src=header_signup&redirect_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start)

- **Role**:
-If your terraform server is in the cloud, then create a role and attach the role to your server.


- Generate Security Credential s using AWS Management Console
  - Go to Services -> IAM -> Users -> "Your-Admin-User" -> Security Credentials -> Create Access Key
- Configure AWS credentials using SSH Terminal on your local desktop

# **Configure AWS Credentials in command line**
```
$ aws configure
AWS Access Key ID [None]: AKIASUF7DEFKSIAWMZ7K
AWS Secret Access Key [None]: WL9G9Tl8lGm7w9t7B3NEDny1+w3N/K5F3HWtdFH/
Default region name [None]: us-west-2
Default output format [None]: json

# Verify if we are able list S3 buckets
aws s3 ls
```
- Verify the AWS Credentials Profile
```
cat $HOME/.aws/credentials
```
#**Command to reset your AWS credentials incase of a credentials error**:

$ for var in AWS_ACCESS_KEY_ID AWS_SECRET_ACCESS_KEY AWS_SESSION_TOKEN AWS_SECURITY_TOKEN ; do eval unset $var ; done

## F) Windows OS - Terraform & AWS CLI Install
- [Download Terraform](https://www.terraform.io/downloads.html)
- [Install CLI](https://learn.hashicorp.com/tutorials/terraform/install-cli)
- Unzip the package
- Create new folder `binaries`
- Copy the `terraform.exe` to a `binaries`
- Set PATH in windows
   **How to set the windows path: Windows 8/10**
          In Search, search for and then select:
          System (Control Panel)
          Click the Advanced system settings link.
          Click Environment Variables.
          In the section System Variables find the PATH environment variable and select it.
          Click Edit. If the PATH environment variable does not exist, click New.
          In the Edit System Variable (or New System Variable) window, specify the value of the PATH environment variable.
          Click OK. Close all remaining windows by clicking OK.

- Install [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)

## Terraform install on windows using a packet manager
-Install terraform on windows using the windows package manager(Use powershell and install as administrator).
    **$ choco install terraform**

## G) Linux OS - Terraform & AWS CLI Install
- [Download Terraform](https://www.terraform.io/downloads.html)
- [Linux OS - Terraform Install](https://learn.hashicorp.com/tutorials/terraform/install-cli)

# Install Terraform on Ubuntu:
     $sudo apt-get update && sudo apt-get install -y gnupg software-properties-common curl
     $curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
     $sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
     $sudo apt-get update && sudo apt-get install terraform

# Install Terraform on RHEL:
      **Install aws cli**
      sudo yum update -y
      sudo yum install curl unzip wget -y  
      curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
      unzip awscliv2.zip
      sudo ./aws/install

      **Install Terraform**
      a) *Download binary*
      sudo yum update -y
      sudo yum install wget unzip -y
      sudo wget https://releases.hashicorp.com/terraform/1.4.4/terraform_1.1.4_linux_amd64.zip
      sudo unzip terraform_1.1.4_linux_amd64.zip -d /usr/local/bin
      terraform -v

      b) *Install from hashicorp repo*
     sudo yum install -y yum-utils
     sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo
     sudo yum -y install terraform




Terraform Command Basics
Step-01: Terraform configuration files
Terraform uses declarative syntax to describe your Infrastructure as Code (IaC) infrastructure and then persist it in configuration files that can be shared, reviewed, edited, versioned, preserved, and reused.
Terraform configuration files can use either of two formats: Terraform domain-specific language (HashiCorp Configuration Language format [HCL]), which is the recommended approach, or JSON format if the files need to be machine-readable.
Configuration files that use the HCL format end with the .tf file extension;
Those using JSON format end with the .tf.json file extension.
The Terraform format is human-readable, while the JSON format is machine readable
Step-01: Introduction to Terraform workflow - main commands
Terraform init: - Used to initialize a working directory containing terraform config files. - This is the first command that should be run after writing a new terraform configuration file. - It downloads providers and modules Terraform validate: - Validates the configuration files in the respective directory to ensure that they are syntactically valid and internally consistent. Terraform plan: - Creates an execution plan - Terraform performs a refresh and determines what actions are necessary to achieve the desired state specified in the configuration files Terraform apply: - Used to apply the changes required to reach the desired state of the configuration - By default, apply scans the current directory for the configuration and applies the changes appropriately. - The state file is created when apply is ran the first time. Terraform destroy: - Use to destroy terraform managed infrastructure. - This will ask for confirmation before destroying.

Step-02: Review terraform manifest for EC2 Instance
Pre-Conditions-1: Ensure you have default-vpc in that respective region
Pre-Conditions-2: Ensure AMI you are provisioning exists in that region if not update AMI ID
Pre-Conditions-3: Verify your AWS Credentials in $HOME/.aws/credentials
# Terraform Settings Block
terraform {
  required_version = "~> 1.0"
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 3.0"            # Optional but recommended in production
    }
  }
}

# Provider Block
provider "aws" {
  profile = "default"
  region  = "us-west-2"
}

# Resource Block
resource "aws_instance" "ec2demo" {
  ami           = "ami-0e5b6b6a9f3db6db8"
  instance_type = "t2.micro"
}
Step-03: Terraform Core Commands
Initialize Terraform
terraform init

Terraform Validate
terraform validate

Terraform Plan to Verify what it is going to create / update / destroy
terraform plan

Terraform Apply to Create EC2 Instance
terraform apply

Step-04: Verify the EC2 Instance in AWS Management Console
Go to AWS Management Console -> Services -> EC2
Verify newly created EC2 instance
Step-05: Destroy Infrastructure
Destroy EC2 Instance
terraform destroy




## **Terraform basic commands**

#**terraform init**
•	initializes a working directory containing Terraform configuration files.
•	performs
      	- backend initialization
        - storage for terraform state file.
        - modules installation,
        - downloaded from terraform registry to local path
        - provider(s) plugins installation,
        - the plugins are downloaded in the sub-directory of the present working directory at the path of .terraform/plugins
•	supports -upgrade to update all previously installed plugins to the newest version that complies with the configuration’s version constraints
•	is safe to run multiple times, to bring the working directory up to date with changes in the configuration
•	does not delete the existing configuration or state

# **terraform validate**
•	validates syntactically for format and correctness.
•	is used to validate/check the syntax of the Terraform files.
•	verifies whether a configuration is syntactically valid and internally consistent, regardless of any provided variables or existing state.
•	A syntax check is done on all the terraform files in the directory, and will display an error if any of the files doesn’t validate.

# **terraform plan**
•	create a execution plan
•	traverses each vertex and requests each provider using parallelism
•	calculates the difference between the last-known state and
the current state and presents this difference as the output of the terraform plan operation to user in their terminal
•	does not modify the infrastructure or state.
•	allows a user to see which actions Terraform will perform prior to making any changes to reach the desired state
•	will scan all *.tf  files in the directory and create the plan
•	will perform refresh for each resource and might hit rate limiting issues as it calls provider APIs
•	all resources refresh can be disabled or avoided using
     	-refresh=false or
       target=xxxx or
       break resources into different directories.
•	supports -out to save the plan

#**terraform apply**
•	apply changes to reach the desired state.
•	scans the current directory for the configuration and applies the changes appropriately.
•	can be provided with a explicit plan, saved as out from terraform plan
•	If no explicit plan file is given on the command line, terraform apply will create a new plan automatically
  and prompt for approval to apply it
•	will modify the infrastructure and the state.
•	if a resource successfully creates but fails during provisioning,
    - Terraform will error and mark the resource as “tainted”.
    - A resource that is tainted has been physically created, but can’t be considered safe to use since provisioning failed.
    - Terraform also does not automatically roll back and destroy the resource during the apply when the failure happens, because that would go against the execution plan: the execution plan would’ve said a resource will be created, but does not say it will ever be deleted.
•	does not import any resource.
•	supports -auto-approve to apply the changes without asking for a confirmation
•	supports -target to apply a specific module

#**terraform refresh**
•	used to reconcile the state Terraform knows about (via its state file) with the real-world infrastructure
•	does not modify infrastructure, but does modify the state file
destroy
•	destroy the infrastructure and all resources
•	modifies both state and infrastructure
•	terraform destroy -target can be used to destroy targeted resources
•	terraform plan -destroy allows creation of destroy plan

#**terraform import**
•	helps import already-existing external resources, not managed by Terraform, into Terraform state and allow it to manage those resources
•	Terraform is not able to auto-generate configurations for those imported modules, for now, and requires you to first write the resource definition in Terraform and then import this resource

#**terraform taint**
•	marks a Terraform-managed resource as tainted, forcing it to be destroyed and recreated on the next apply.
•	will not modify infrastructure, but does modify the state file in order to mark a resource as tainted. Infrastructure and state are changed in next apply.
•	can be used to taint a resource within a module

#**terraform fmt**
•	format to lint the code into a standard format

#**terraform console**
•	command provides an interactive console for evaluating expressions.




The AWS provider offers a flexible means of providing credentials for authentication. The following methods are supported, in this order, and explained below:

- **Static credentials**
     provider "aws" {
       region     = "us-west-2"
       access_key = "my-access-key"
       secret_key = "my-secret-key"
    }
    
- **Environment variables**
     $ export AWS_ACCESS_KEY_ID="accesskey"
     $ export AWS_SECRET_ACCESS_KEY="secretkey"
     $ export AWS_DEFAULT_REGION="us-west-2"

- **Shared credentials/configuration file**
    provider "aws" {
      region                  = "us-west-2"
      shared_credentials_file = "/Users/tf_user/.aws/creds"
      profile                 = "dev"
  }




# Terraform Configuration Language Syntax

## **Step-01: Blocks**
https://www.terraform.io/docs/configuration/syntax.html
# a) **Understand Blocks**
      - Terraform Settings Block
      - Provider Block
      - Resource Block
      - Input Variables Block
      - Output Values Block
      - Local Values Block
      - Data Sources Block
      - Modules Block

- A block is a container for other content:
# Template

     <BLOCK TYPE> "<BLOCK LABEL>" "<BLOCK LABEL>"   {
       # Block body
      <IDENTIFIER> = <EXPRESSION> # Argument
     }

# AWS Example
resource "aws_instance" "ec2demo" {
  # BLOCK BODY
  ami           = "ami-04d29b6f966df1537" # Argument
  instance_type = var.instance_type # Argument with value as expression (Variable value replaced from varibales.tf

      network_interface {
       # ...
    }
  }

- A block has a type (resource in this example). Each block type defines how many labels must follow the type keyword. The resource block type expects two labels, which are aws_instance and ec2demo in the example above. A particular block type may have any number of required labels, or it may require none as with the nested network_interface block type.

- After the block type keyword and any labels, the block body is delimited by the { and } characters. Within the block body, further arguments and blocks may be nested, creating a hierarchy of blocks and their associated arguments.

## **Step-02: Arguments, Expressions, Attributes & Meta-Arguments**

# Arguments
  -They assign a value to a name. They appear within blocks. Arguments can be required or optional.

# Expressions
- They represent a value, either literally or by referencing and combining other values. They appear as values for arguments, or within other expressions.

# Attributes
- They represent a named piece of data that belongs to some kind of object. The value of an attribute can be referenced in expressions using a dot-separated notation, like aws_instance.example.id.
- The format looks like `resource_type.resource_name.attribute_name`

# Identifiers
- Argument names, block type names, and the names of most Terraform-specific constructs like resources, input variables, etc. are all identifiers.

- Identifiers can contain letters, digits, underscores (_), and hyphens (-). The first character of an identifier must not be a digit, to avoid ambiguity with literal numbers.

# Comments
- The Terraform language supports three different syntaxes for comments:

The # begins a single-line comment, ending at the end of the line.
// also begins a single-line comment, as an alternative to #.
/* and */ are start and end delimiters for a comment that might span over multiple lines.
The # single-line comment style is the default comment style and should be used in most cases. Automatic configuration formatting tools may automatically transform // comments into # comments, since the double-slash style is not idiomatic.

# Meta-Arguments
(https://www.terraform.io/docs/language/meta-arguments/)
- Meta-Arguments change a resource type's behavior (Example: count, for_each)

 **depends_on**
   - The depends_on meta-argument, if present, must be a list of references to other resources or child modules in the same calling module. Arbitrary expressions are not allowed in the depends_on argument value, because its value must be known before Terraform knows resource relationships and thus before it can safely evaluate expressions.

 **Count**
   - The count meta-argument accepts numeric expressions. However, unlike most arguments, the count value must be known before Terraform performs any remote resource actions. This means count can't refer to any resource attributes that aren't known until after a configuration is applied
   - In blocks where count is set, an additional count object is available in expressions, so you can modify the configuration of each instance. This object has one attribute: **count.index** — The distinct index number (starting with 0) corresponding to this instance.

 **for_each**
  - If your instances are almost identical, count is appropriate. If some of their arguments need distinct values that can't be directly derived from an integer, it's safer to use for_each.
  - The for_each meta-argument accepts a map or a set of strings, and creates an instance for each item in that map or set. Each instance has a distinct infrastructure object associated with it, and each is separately created, updated, or destroyed when the configuration is applied.
  - In blocks where for_each is set, an additional each object is available in expressions, so you can modify the configuration of each instance. This object has two attributes:

      each.key — The map key (or set member) corresponding to this instance.
      each.value — The map value corresponding to this instance. (If a set was provided, this is the same as each.key.)
  - The for_each value must be a map or set with one element per desired resource instance. When providing a set, you must use an expression that explicitly returns a set value, like the toset function; to prevent unwanted surprises during conversion, the for_each argument does not implicitly convert lists or tuples to sets.
  -toset converts its argument to a set value. Explicit type conversions are rarely necessary in Terraform because it will convert types automatically where required. Use the explicit type conversion functions only to normalize types returned in module outputs. Pass a list value to toset to convert it to a set, which will remove any duplicate elements and discard the ordering of the elements.

  # map
  resource "azurerm_resource_group" "rg" {
    for_each = {
      a_group = "eastus"
      another_group = "westus2"
    }
    name     = each.key
    location = each.value
  }

  # Set of strings
    resource "aws_iam_user" "the-accounts" {
      for_each = toset( ["Todd", "James", "Alice", "Dottie"] )
      name     = each.key
   }

 **lifecycle**




#Block-1: **Terraform Settings Block**
terraform {
  required_version = "~> 1.0"         1.1.4/5/6/7   1.2/3/4/5 1.1.4/5/6/7
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 3.0"
    }
  }

  
  # Adding Backend as S3 for Remote State Storage with State Locking
  backend "s3" {
    bucket = "terraform-mylandmark"
    key    = "prod/terraform.tfstate"
    region = "us-west-2"
    # For State Locking
    dynamodb_table = "terraform-lock"
  }
}

resource "aws_dynamodb_table" “tf_lock" {
  name = "terraform-lock"
  hash_key = "LockID"
  read_capacity = 3
  write_capacity = 3
  attribute {
     name = "LockID"
     type = "S"
   }
  tags  {
    Name = "Terraform Lock Table"
   }
 }


# Block-2: **Provider Block**
provider "aws" {
  profile = "default" # AWS Credentials Profile configured on your local desktop terminal  $HOME/.aws/credentials
  region  = "us-west-2"
}

# Block-3: **Resource Block**
resource "aws_instance" "class25" {
  ami           = "ami-0e5b6b6a9f3db6db8" # Amazon Linux
  instance_type = var.instance_type
}

# Block-4: **Input Variables Block**
variable "instance_type" {
  default = "t2.micro"
  description = "EC2 Instance Type"
  type = string
}

# Block-5: **Output Values Block**
output "ec2_instance_publicip" {
  description = "EC2 Instance Public IP"
  value = aws_instance.class25.public_ip
}

# Block-6: **Local Values Block**
# Create S3 Bucket - with Input Variables & Local Values
locals {
  name = "${var.app_name}-${var.environment_name}"
}
bucket_name = locals.name


# Block-7: **Data sources Block**
# Get latest AMI ID for Amazon Linux2 OS
data "aws_ami" "amzlinux" {
  most_recent      = true
  owners           = ["amazon"]

  filter {
    name   = "name"
    values = ["amzn2-ami-hvm-*"]
  }

  filter {
    name   = "root-device-type"
    values = ["ebs"]
  }

  filter {
    name   = "virtualization-type"
    values = ["hvm"]
  }

  filter {
    name   = "architecture"
    values = ["x86_64"]
  }

}


# Block-8: **Modules Block**
# AWS EC2 Instance Module

module "ec2_cluster" {
  source                 = "terraform-aws-modules/ec2-instance/aws"
  version                = "~> 2.0"

  name                   = "my-modules-demo"
  instance_count         = 2

  ami                    = data.aws_ami.amzlinux.id
  instance_type          = "t2.micro"
  key_name               = "terraform-key"
  monitoring             = true
  vpc_security_group_ids = ["sg-08b25c5a5bf489ffa"]  # Get Default VPC Security Group ID and replace
  subnet_id              = "subnet-4ee95470" # Get one public subnet id from default vpc and replace
  user_data               = file("apache-install.sh")

  tags = {
    Terraform   = "true"
    Environment = "dev"
  }
}



# Terraform Settings, Providers & Resource Blocks
## Step-01: Introduction
- [Terraform Settings](https://www.terraform.io/docs/language/settings/index.html)
- [Terraform Providers](https://www.terraform.io/docs/providers/index.html)
- [Terraform Resources](https://www.terraform.io/docs/language/resources/index.html)
- [Terraform File Function](https://www.terraform.io/docs/language/functions/file.html)
- Create EC2 Instance using Terraform and provision a webserver with userdata.

## Step-02: In versions.tf - Create Terraform Settings Block
- Understand about [Terraform Settings Block](https://www.terraform.io/docs/language/settings/index.html) and create it
```t
terraform {
  required_version = "~> 0.14." # which means any version equal & above 0.14 like 0.15, 0.16 etc and < 1.xx
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 3.0"
    }
  }
}
```

## Step-03: In versions.tf - Create Terraform Providers Block
- Understand about [Terraform Providers](https://www.terraform.io/docs/providers/index.html)
- Configure AWS Credentials in the AWS CLI if not configured
```t
# Verify AWS Credentials
cat $HOME/.aws/credentials
```
- Create [AWS Providers Block](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#authentication)
```t
# Provider Block
provider "aws" {
  region  = us-west-2
  profile = "default"
}
```

## Step-04: In ec2instance.tf -  Create Resource Block
- Understand about [Resources](https://www.terraform.io/docs/language/resources/index.html)
- Create [EC2 Instance Resource](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance)
- Understand about [File Function](https://www.terraform.io/docs/language/functions/file.html)
- Understand about [Resources - Argument Reference](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance#argument-reference)
- Understand about [Resources - Attribute Reference](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance#attributes-reference)
```t
# Resource: EC2 Instance
resource "aws_instance" "myec2vm" {
  ami = "ami-0533f2ba8a1995cf9"
  instance_type = "t3.micro"
  user_data = file("${path.module}/app1-install.sh")
  tags = {
    "Name" = "EC2 Demo"
  }
}
```


## Step-05: Review file app1-install.sh
```sh
#! /bin/bash
# Instance Identity Metadata Reference - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-identity-documents.html
sudo yum update -y
sudo yum install -y httpd
sudo systemctl enable httpd
sudo service httpd start  
sudo echo '<h1>Welcome to Landmark Technologies</h1>' | sudo tee /var/www/html/index.html
sudo mkdir /var/www/html/app1
sudo echo '<!DOCTYPE html> <html> <body style="background-color:rgb(250, 210, 210);"> <h1>Welcome to Landmark Technologies</h1> <p>Terraform Demo</p> <p>Application Version: V1</p> </body></html>' | sudo tee /var/www/html/app1/index.html
sudo curl http://169.254.169.254/latest/dynamic/instance-identity/document -o /var/www/html/app1/metadata.html
```

## Step-06: Execute Terraform Commands
```t
# Terraform Initialize
terraform init
Observation:
1) Initialized Local Backend
2) Downloaded the provider plugins (initialized plugins)
3) Review the folder structure ".terraform folder"

# Terraform Validate
terraform validate
Observation:
1) If any changes to files, those will come as printed in stdout (those file names will be printed in CLI)

# Terraform Plan
terraform plan
Observation:
1) No changes - Just prints the execution plan

# Terraform Apply
terraform apply
[or]
terraform apply -auto-approve
Observations:
1) Create resources on cloud
2) Created terraform.tfstate file when you run the terraform apply command
```

## Step-07: Access Application
- **Important Note:** verify if default VPC security group has a rule to allow port 80
```t
# Access index.html
http://<PUBLIC-IP>/index.html
http://<PUBLIC-IP>/app1/index.html

# Access metadata.html
http://<PUBLIC-IP>/app1/metadata.html
```

## Step-08: Terraform State - Basics
- Understand about Terraform State
- Terraform State file `terraform.tfstate`
- Understand about `Desired State` and `Current State`


## Step-09: Clean-Up
```t
# Terraform Destroy
terraform plan -destroy  # You can view destroy plan using this command
terraform destroy

# Clean-Up Files
rm -rf .terraform*
rm -rf terraform.tfstate*
```


## Step-10: Additional Observations - Concepts we will learn in next section
- EC2 Instance created we didn't associate a EC2 Key pair to login to EC2 Instance
  - Terraform Resource Argument - `Key Name`
- AMI Name is static - How to make it Dynamic ?
  - Use `Terraform Datasources` concept
- We didn't create multiple instances of same EC2 Instance
  - Resource Meta-Argument: `count`
- We didn't add any variables for parameterizations
  - Terraform `Input Variable` Basics
- We didn't extract any information on terminal about instance information
  -  Terraform `Outputs`
- Create second resource only after first resource is created
  - Defining Explicit Dependency in Terraform using Resource Meta-Argument `depends_on`



# Terraform Variables and Datasources

## Step-00: Pre-requisite Note
- Create a `key pair` in AWS EC2 Key pairs which we will reference in our EC2 Instance

## Step-01: Introduction
### Terraform Concepts
- Terraform Input Variables
- Terraform Datasources
- Terraform Output Values

### What are we going to learn ?
1. Learn about Terraform `Input Variable` basics
  - AWS Region
  - Instance Type
  - Key Name
2. Define `Security Groups` and Associate them as a `List item` to AWS EC2 Instance  
  - vpc-ssh
  - vpc-web
3. Learn about Terraform `Output Values`
  - Public IP
  - Public DNS
4. Get latest EC2 AMI ID Using `Terraform Datasources` concept
5. We are also going to use existing EC2 Key pair `Automationkey`
6. Use all the above to create an EC2 Instance in default VPC


## Step-02: c2-variables.tf - Define Input Variables in Terraform
- [Terraform Input Variables](https://www.terraform.io/docs/language/values/variables.html)

```t
# AWS Region
variable "aws_region" {
  description = "Region in which AWS Resources to be created"
  type = string
  default = "us-east-1"  
}

# AWS EC2 Instance Type
variable "instance_type" {
  description = "EC2 Instance Type"
  type = string
  default = "t3.micro"  
}

# AWS EC2 Instance Key Pair
variable "instance_keypair" {
  description = "AWS EC2 Key pair that need to be associated with EC2 Instance"
  type = string
  default = "terraform-key"
}
```
- Reference the variables in respective `.tf`fies
```t
# versions.tf
region  = var.aws_region

# ec2instance.tf
instance_type = var.instance_type
key_name = var.instance_keypair  
```

## Step-03: ec2securitygroups.tf - Define Security Group Resources in Terraform
- [Resource: aws_security_group](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group)
```t
# Create Security Group - SSH Traffic
resource "aws_security_group" "vpc-ssh" {
  name        = "vpc-ssh"
  description = "Dev VPC SSH"
  ingress {
    description = "Allow Port 22"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  egress {
    description = "Allow all ip and ports outboun"
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

# Create Security Group - Web Traffic
resource "aws_security_group" "vpc-web" {
  name        = "vpc-web"
  description = "Dev VPC web"
  ingress {
    description = "Allow Port 80"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    description = "Allow Port 443"
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    description = "Allow all ip and ports outbound"
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```
- Reference the security groups in `ec2instance.tf` file as a list item
```t
# List Item
vpc_security_group_ids = [aws_security_group.vpc-ssh.id, aws_security_group.vpc-web.id]  
```

## Step-04: ami-datasource.tf - Define Get Latest AMI ID for Amazon Linux2 OS
- [Data Source: aws_ami](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/ami)
```t
# Get latest AMI ID for Amazon Linux2 OS
# Get Latest AWS AMI ID for Amazon2 Linux
data "aws_ami" "amzlinux2" {
  most_recent = true
  owners = [ "amazon" ]
  filter {
    name = "name"
    values = [ "amzn2-ami-hvm-*-gp2" ]
  }
  filter {
    name = "root-device-type"
    values = [ "ebs" ]
  }
  filter {
    name = "virtualization-type"
    values = [ "hvm" ]
  }
  filter {
    name = "architecture"
    values = [ "x86_64" ]
  }
}
```
- Reference the datasource in `c5-ec2instance.tf` file
```t
# Reference Datasource to get the latest AMI ID
ami = data.aws_ami.amzlinux2.id
```

## Step-05: c5-ec2instance.tf - Define EC2 Instance Resource
- [Resource: aws_instance](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance)
```t
# EC2 Instance
resource "aws_instance" "myec2vm" {
  ami = data.aws_ami.amzlinux2.id
  instance_type = var.instance_type
  user_data = file("${path.module}/app1-install.sh")
  key_name = var.instance_keypair
  vpc_security_group_ids = [aws_security_group.vpc-ssh.id, aws_security_group.vpc-web.id]  
  tags = {
    "Name" = "EC2 Demo 2"
  }
}
```


## Step-06: c6-outputs.tf - Define Output Values
- [Output Values](https://www.terraform.io/docs/language/values/outputs.html)
```t
# Terraform Output Values
output "instance_publicip" {
  description = "EC2 Instance Public IP"
  value = aws_instance.myec2vm.public_ip
}

output "instance_publicdns" {
  description = "EC2 Instance Public DNS"
  value = aws_instance.myec2vm.public_dns
}
```

## Step-07: Execute Terraform Commands
```t
# Terraform Initialize
terraform init
Observation:
1) Initialized Local Backend
2) Downloaded the provider plugins (initialized plugins)
3) Review the folder structure ".terraform folder"

# Terraform Validate
terraform validate
Observation:
1) If any changes to files, those will come as printed in stdout (those file names will be printed in CLI)

# Terraform Plan
terraform plan
Observation:
1) Verify the latest AMI ID picked and displayed in plan
2) Verify the number of resources that going to get created
3) Verify the variable replacements worked as expected

# Terraform Apply
terraform apply
[or]
terraform apply -auto-approve
Observations:
1) Create resources on cloud
2) Created terraform.tfstate file when you run the terraform apply command
3) Verify the EC2 Instance AMI ID which got created
```

## Step-08: Access Application
```t
# Access index.html
http://<PUBLIC-IP>/index.html
http://<PUBLIC-IP>/app1/index.html

# Access metadata.html
http://<PUBLIC-IP>/app1/metadata.html
```

## Step-09: Clean-Up
```t
# Terraform Destroy
terraform plan -destroy  # You can view destroy plan using this command
terraform destroy

# Clean-Up Files
rm -rf .terraform*
rm -rf terraform.tfstate*
```



## **Variable files**

- Values for the input variables of a root module can be gathered in variable definition files and passed together using the -var-file=FILE option.

- For all files which match terraform.tfvars or *.auto.tfvars present in the current directory, Terraform automatically loads them to populate variables. If the file is located somewhere else, you can pass the path to the file using the -var-file flag. It is recommended to name such files with names ending in .tfvars.

- The -var-file flag can be used multiple times per command invocation:

    $ terraform apply -var-file=foo.tfvars -var-file=bar.tfvars

- According to the terraform documentation on input variables, Terraform loads variables in the following order, with later sources taking precedence over earlier ones:

    - Environment variables
    - The tfvarsfile, if present.
    - The tfvars.jsonfile, if present.
    - Any *.auto.tfvars or *.auto.tfvars.json files, processed in lexical order of their filenames.
    Any -var and -var-file options on the command line, in order they are provided. (This includes variables set by a Terraform Cloud workspace.)

# **Environmental variables**

- When Terraform runs, it looks in your environment for variables that match the pattern TF_VAR_<VARIABLE_NAME>, and assigns those values to the corresponding Terraform variables in your configuration.
- Assign values to the database administrator username and password using environment variables.

  $ export TF_VAR_db_username=admin TF_VAR_db_password=adifferentpassword

# **.tfvars file**
- Terraform supports setting variable values with variable definition (.tfvars) files. You can use multiple variable definition files, and many practitioners use a separate file to set sensitive or secret values.
- Create a new file called secret.tfvars to assign values to the new variables.

      db_username = "admin"
      db_password = "insecurepassword"

- Apply these changes using the -var-file parameter. Respond to the confirmation prompt with yes.

    $ terraform apply -var-file="secret.tfvars"




## **Variables**

- A variable is a value that can change, depending on conditions or on information passed to the program.
- Variables are used to store information to be referenced and manipulated in a computer program.
- They also provide a way of labeling data with a descriptive name, so our programs can be understood more clearly by the reader and ourselves.
- It is helpful to think of variables as containers that hold information. Their sole purpose is to label and store data in memory. This data can then be used throughout your program.

The following example shows the variable types that are supported by terraform.

#**String**
 - Strings are usually represented by a double-quoted sequence of Unicode characters, "like this"
```t
variable "vpcname" {
  type    = string
  default = "myvpc"
}

```
#**Number**

- Numbers are represented by unquoted sequences of digits with or without a decimal point, like 15 or 6.283185.
```t
variable "sshport" {
  type    = number
  default = 22
}
```

#**Boolean**
- Bools are represented by the unquoted symbols true and false.
```t
variable "enabled" {
  default = false
}
```
#**List**
- Lists is represented by a pair of square brackets containing a comma-separated sequence of values, like ["a", 15, true].
```t
variable "mylist" {
  type    = list(string)
  default = ["Value1", "Value2"]
}
```
#How to reference List values ?

instance_type = var.mylist[1]

#**Map**
- Maps/objects are represented by a pair of curly braces containing a series of <KEY> = <VALUE> pairs:
```T
variable "mymap" {
  type = map
  default = {
    Key1 = "Value1"
    Key2 = "Value2"
  }
}
```
#How to reference Map values ?
 
instance_type = var.mymap["key1"]

#**Input**
 ```t
variable "inputname" {
  type        = string
  description = "Set the name of the VPC"
}
```
- note that if no default value is provided, then the variable will be an input variable and will prompt you to enter a value at runtime.

 ```t
resource "aws_vpc" "myvpc" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = var.inputname
  }
}
```
#**Output**
```t
output "vpcid" {
  value = aws_vpc.myvpc.id
}
```
#**Tuple**
- Lists/tuples are represented by a pair of square brackets containing a comma-separated sequence of values, like ["a", 15, true].
```t
variable "mytuple" {
  type    = tuple([string, number, string])
  default = ["cat", 1, "dog"]
}
```
#**Objects**
```t
variable "myobject" {
  type = object({ name = string, port = list(number) })
  default = {
    name = "Landmark"
    port = [22, 25, 80]
  }
}
```
#**Variables with Lists and Maps**

#AWS EC2 Instance Type - List
```t
 variable "instance_type_list" {
  description = "EC2 Instance Type"
  type = list(string)
  default = ["t3.micro", "t3.small"]
}

#instance_type = var.instance_type_list[0]
```
 
#AWS EC2 Instance Type - Map
```t
 variable "instance_type_map" {
  description = "EC2 Instance Type"
  type = map(string)
  default = {
    "dev" = "t3.micro"
    "qa"  = "t3.small"
    "prod" = "t3.large"
  }
}

#instance_type = var.instance_type_map["qa"]
```


# Terraform For Loops, Lists, Maps and Count Meta-Argument

## Step-00: Pre-requisite Note
- We are using the `default vpc` in `us-west-2` region

## Step-01: Introduction
- Terraform Meta-Argument: `Count`
- **Terraform Lists & Maps**
  - List(string)
  - map(string)
- **Terraform for loops**
  - for loop with List
  - for loop with Map
  - for loop with Map Advanced
- **Splat Operators**
  - Legacy Splat Operator `.*.`
  - Generalized Splat Operator (latest)
  - Understand about Terraform Generic Splat Expression `[*]` when dealing with `count` Meta-Argument and multiple output values



## Step-02: variables.tf - Lists and Maps
```t
# AWS EC2 Instance Type - List
variable "instance_type_list" {
  description = "EC2 Instance Type"
  type = list(string)
  default = ["t3.micro", "t3.small"]
}


# AWS EC2 Instance Type - Map
variable "instance_type_map" {
  description = "EC2 Instance Type"
  type = map(string)
  default = {
    "dev" = "t3.micro"
    "qa"  = "t3.small"
    "prod" = "t3.large"
  }
}
```

## Step-04: ec2securitygroups.tf and ami-datasource.tf
- No changes to both files

## Step-05: ec2instance.tf
```t
# How to reference List values ?
instance_type = var.instance_type_list[1]

# How to reference Map values ?
instance_type = var.instance_type_map["prod"]

# Meta-Argument Count
count = 2

# count.index
  tags = {
    "Name" = "Count-Demo-${count.index}"
  }
```

## Step-06: outputs.tf
- for loop with List
- for loop with Map
- for loop with Map Advanced
```t

# Output - For Loop with List
output "for_output_list" {
  description = "For Loop with List"
  value = [for instance in aws_instance.myec2vm: instance.public_dns ]
}

# Output - For Loop with Map
output "for_output_map1" {
  description = "For Loop with Map"
  value = {for instance in aws_instance.myec2vm: instance.id => instance.public_dns}
}

# Output - For Loop with Map Advanced
output "for_output_map2" {
  description = "For Loop with Map - Advanced"
  value = {for c, instance in aws_instance.myec2vm: c => instance.public_dns}
}

# Output Legacy Splat Operator (latest) - Returns the List
output "legacy_splat_instance_publicdns" {
  description = "Legacy Splat Expression"
  value = aws_instance.myec2vm.*.public_dns
}  

# Output Latest Generalized Splat Operator - Returns the List
output "latest_splat_instance_publicdns" {
  description = "Generalized Splat Expression"
  value = aws_instance.myec2vm[*].public_dns
}
```

## Step-07: Execute Terraform Commands
```t
# Terraform Initialize
terraform init

# Terraform Validate
terraform validate

# Terraform Plan
terraform plan
Observations:
1) play with Lists and Maps for instance_type

# Terraform Apply
terraform apply -auto-approve
Observations:
1) Two EC2 Instances (Count = 2) of a Resource myec2vm will be created
2) Count.index will start from 0 and end with 1 for VM Names
3) Review outputs in detail (for loop with list, maps, maps advanced, splat legacy and splat latest)
```

## Step-08: Terraform Comments
- Single Line Comments - `#` and `//`
- Multi-line Commnets - `Start with /*` and `end with */`
- We are going to comment the legacy splat operator, which might be decommissioned in future versions
```t
# Output Legacy Splat Operator (latest) - Returns the List
/* output "legacy_splat_instance_publicdns" {
  description = "Legacy Splat Expression"
  value = aws_instance.myec2vm.*.public_dns
}  */
```

## Step-09: Clean-Up
```t
# Terraform Destroy
terraform destroy -auto-approve

# Files
rm -rf .terraform*
rm -rf terraform.tfstate*
```


## **Sensitive values in state**

- When you run Terraform commands with a local state file, Terraform stores the state as plain text, including variable values, even if you have flagged them as sensitive. Terraform needs to store these values in your state so that it can tell if you have changed them since the last time you applied your configuration.
- Since Terraform state can contain sensitive values, you must keep your state file secure to avoid exposing this data. Refer to the Terraform documentation to learn more about securing your state file.

## **Backend**
- Each Terraform configuration can specify a backend, which defines exactly where and how operations are performed, where state snapshots are stored, etc.

- If a configuration includes no backend block, Terraform defaults to using the local backend, which performs operations on the local system and stores state as a plain file in the current working directory.

- When changing backends, Terraform will give you the option to migrate your state to the new backend. This lets you adopt backends without losing any existing state.

- You can change your backend configuration at any time. You can change both the configuration itself as well as the type of backend (for example from "consul" to "s3").

- Terraform will automatically detect any changes in your configuration and request a reinitialization. As part of the reinitialization process, Terraform will ask if you'd like to migrate your existing state to the new configuration. This allows you to easily switch from one backend to another.

# **S3 Backend (with locking via DynamoDB)**
- Stores the state as a given key in a given bucket on Amazon S3. This backend also supports state locking and consistency checking via Dynamo DB, which can be enabled by setting the dynamodb_table field to an existing DynamoDB table name. A single DynamoDB table can be used to lock multiple remote state files. Terraform generates key names that include the values of the bucket and key variables.

- It is highly recommended that you enable Bucket Versioning on the S3 bucket to allow for state recovery in the case of accidental deletions and human error.

##**DynamoDB State Locking**
The following configuration is optional:

**dynamodb_table**
- (Optional) Name of DynamoDB Table to use for state locking and consistency. The table must have a primary key named LockID with type of string. If not configured, state locking will be disabled.

# **DynamoDB Table Permissions**
If you are using state locking, Terraform will need the following AWS IAM permissions on the DynamoDB table (arn:aws:dynamodb:::table/mytable):

     dynamodb:GetItem
     dynamodb:PutItem
     dynamodb:DeleteItem


##**Data Source configurations**
- To make use of the S3 remote state in another configuration, use the terraform_remote_state data source.

data "terraform_remote_state" "network" {
  backend = "s3"
  config = {
    bucket = "terraform-state-prod"
    key    = "network/terraform.tfstate"
    region = "us-east-1"
  }
}








