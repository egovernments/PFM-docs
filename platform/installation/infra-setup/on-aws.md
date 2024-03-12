# On AWS

The [**Amazon Elastic Kubernetes Service (EKS)**](https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html) is one of the AWS services for deploying, managing, and scaling any distributed and containerized workloads, here we can provision the EKS cluster on AWS from ground up and using an automated way (infra-as-code) using [**terraform**](https://www.terraform.io/intro/index.html) and then deploy the DIGIT-iFIX Services config-as-code using [**Helm**](https://helm.sh/docs/).

## Pre-reads <a href="#pre-read" id="pre-read"></a>

* Know about EKS: [https://www.youtube.com/watch?v=SsUnPWp5ilc](https://www.youtube.com/watch?v=SsUnPWp5ilc)
* Know what is terraform: [https://youtu.be/h970ZBgKINg](https://youtu.be/h970ZBgKINg)

## Pre-requisites <a href="#prerequisites" id="prerequisites"></a>

1. ​[**AWS account**](https://portal.aws.amazon.com/billing/signup?nc2=h\_ct\&src=default\&redirect\_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start) with the admin access to provision EKS Service, you can always subscribe to free AWS account to learn the basics and try, but there is a limit to [**what is offered as free**](https://aws.amazon.com/free/), for this demo you need to have a commercial subscription to the EKS service.
2. Install [**kubectl**](https://kubernetes.io/docs/tasks/tools/) on your local machine that helps you interact with the kubernetes cluster
3. &#x20;Install [**Helm**](https://helm.sh/docs/intro/install/) that helps you package the services along with the configurations, envs, secrets, etc into a [**kubernetes manifests**](https://devspace.cloud/docs/cli/deployment/kubernetes-manifests/what-are-manifests)
4. Install [**terraform**](https://releases.hashicorp.com/terraform/0.14.10/) version (0.14.10) for the Infra-as-code (IaC) to provision cloud resources as code and with desired resource graph and also it helps to destroy the cluster at one go.
5. **​**[**Install AWS CLI**](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html) on your local machine so that you can use aws cli commands to provision and manage the cloud resources on your account.
6. Install [**AWS IAM Authenticator**](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html) that helps you authenticate your connection from your local machine so that you should be able to deploy DIGIT services.
7.  Use the [**AWS IAM User**](https://docs.aws.amazon.com/IAM/latest/UserGuide/id\_users\_create.html) **credentials provided** for the Terraform ([**Infra-as-code**](https://devops.digit.org/devops-general/infra-as-code)) to connect with your AWS account and provision the cloud resources.

    ​

    * You'll get a **Secret Access Key** and **Access Key ID**. **Save them safely.**
    * Open the terminal and run the following command. The AWS CLI is already installed and the credentials are saved. (Provide the credentials and you can leave the region and output format blank).

    ```
    aws configure --profile mgramseva-infra-account 

    AWS Access Key ID []:<Your access key>
    AWS Secret Access Key []:<Your secret key>
    Default region name []: ap-south-1
    Default output format []: text
    ```

    The above will create the following file In your machine as /Users/.aws/credentials

    ```
    [mgramseva-infra-account] 
    aws_access_key_id=*********** 
    aws_secret_access_key=****************************
    ```

Before we provision the cloud resources, we need to understand and be sure about what resources need to be provisioned by terraform to deploy DIGIT. The following picture shows the various key components. (EKS, Worker Nodes, Postgress DB, EBS Volumes, Load Balancer)

![EKS Architecture for mGramSeva Setup](https://gblobscdn.gitbook.com/assets%2F-MEQnEQWBZ6Gjip-3pEg%2F-Md1lfe6NwE0P1OdZlxg%2F-Md1rBSubx1ny2pReDeE%2Fimage.png?alt=media\&token=45a75d9d-f45a-466c-9298-9c1db825cd8d)

Considering the above deployment architecture, the following is the resource graph that we are going to provision using terraform in a standard way so that every time and for every environment, it'll have the same infra.

* EKS Control Plane (Kubernetes Master)
* Work node group (VMs with the estimated number of vCPUs, Memory)
* Node-pool's (mgramseva and ifix)
* EBS Volumes (persistent volumes)
* RDS (Postgresql)
* VPCs (private network)
* Users to access, deploy and read-only

## Understand The **Resource Graph In** Terraform Script <a href="#set-up-and-initialize-your-terraform-workspace-1" id="set-up-and-initialize-your-terraform-workspace-1"></a>

* Ideally, one would write the terraform script from the scratch using this [doc](https://learn.hashicorp.com/collections/terraform/modules).
* Here we have already written the terraform script that provisions the production-grade DIGIT Infra and can be customized with the specified configuration.
* Let's clone the [iFix-DevOps](https://github.com/misdwss/iFix-DevOps) GitHub repo where the terraform script to provision EKS cluster is available and below is the structure of the files.

```
git clone https://github.com/misdwss/iFix-DevOps.git
cd iFix-DevOps/infra-as-code/terraform


└── modules
    ├── db
    │   └── aws
    │       ├── main.tf
    │       ├── outputs.tf
    │       └── variables.tf
    ├── kubernetes
    │   └── aws
    │       ├── eks-cluster
    │       │   ├── main.tf
    │       │   ├── outputs.tf
    │       │   └── variables.tf
    │       ├── network
    │       │   ├── main.tf
    │       │   ├── outputs.tf
    │       │   └── variables.tf
    │       └── workers
    │           ├── main.tf
    │           ├── outputs.tf
    │           └── variables.tf
    └── storage
        └── aws
            ├── main.tf
            ├── outputs.tf
            └── variables.tf
```

**Example:**

* **VPC Resources:**
  * VPC
  * Subnets
  * Internet Gateway
  * Route Table
* **EKS Cluster Resources:**
  * IAM Role to allow EKS service to manage other AWS services
  * EC2 Security Group to allow networking traffic with EKS cluster
  * EKS Cluster
* **EKS Worker Nodes Resources:**
  * IAM role allowing Kubernetes actions to access other AWS services
  * EC2 Security Group to allow networking traffic
  * Data source to fetch the latest EKS worker AMI
  * AutoScaling Launch Configuration to configure worker instances
  * AutoScaling Group to launch worker instances
* **Database**
  * Configuration in this directory creates a set of RDS resources including DB instance, DB subnet group, and DB parameter group.
* **Storage Module**
  * Configuration in this directory creates EBS volume and attaches it together.​

The following main.tf with create s3 bucket to store all the state of the execution to keep track.

&#x20;iFix-DevOps/Infra-as-code/terraform/sample-eks/remote-state

&#x20;[**main.tf**](https://github.com/egovernments/DIGIT-DevOps/blob/release/infra-as-code/terraform/sample-aws/remote-state/main.tf)**​**

```
provider "aws" {
  region = "ap-south-1"
}

#This is a bucket name that you can name as you wish
resource "aws_s3_bucket" "terraform_state" {
  bucket = "try-workshop-yourname" 

  versioning {
    enabled = true
  }

  lifecycle {
    prevent_destroy = true
  }
}

#This is a bucket name that you can name as you wish
resource "aws_dynamodb_table" "terraform_state_lock" {
  name           = "try-workshop-yourname"
  read_capacity  = 1
  write_capacity = 1
  hash_key       = "LockID"

  attribute {
    name = "LockID"
    type = "S"
  }
}
```

2\. The following main.tf contains the detailed resource definitions that need to be provisioned, please have a look at it.

&#x20;Dir: iFix-DevOps/Infra-as-code/terraform/sample-eks

&#x20;[**main.tf**](https://github.com/egovernments/DIGIT-DevOps/blob/release/infra-as-code/terraform/sample-aws/main.tf)

```
terraform {
  backend "s3" {
    bucket = "try-workshop-yourname"
    key = "terraform"
    region = "ap-south-1"
  }
}

module "network" {
  source             = "../modules/kubernetes/aws/network"
  vpc_cidr_block     = "${var.vpc_cidr_block}"
  cluster_name       = "${var.cluster_name}"
  availability_zones = "${var.network_availability_zones}"
}


module "iam_user_deployer" {
  source  = "terraform-aws-modules/iam/aws//modules/iam-user"

  name          = "${var.cluster_name}-kube-deployer"
  force_destroy = true  
  create_iam_user_login_profile = false
  create_iam_access_key         = true

  # User "egovterraform" has uploaded his public key here - https://keybase.io/egovterraform/pgp_keys.asc
  pgp_key = "${var.iam_keybase_user}"
}

module "iam_user_admin" {
  source  = "terraform-aws-modules/iam/aws//modules/iam-user"

  name          = "${var.cluster_name}-kube-admin"
  force_destroy = true  
  create_iam_user_login_profile = false
  create_iam_access_key         = true

  # User "egovterraform" has uploaded his public key here - https://keybase.io/egovterraform/pgp_keys.asc
  pgp_key = "${var.iam_keybase_user}"
}

module "iam_user_user" {
  source  = "terraform-aws-modules/iam/aws//modules/iam-user"

  name          = "${var.cluster_name}-kube-user"
  force_destroy = true  
  create_iam_user_login_profile = false
  create_iam_access_key         = true

  # User "test" has uploaded his public key here - https://keybase.io/test/pgp_keys.asc
  pgp_key = "${var.iam_keybase_user}"
}

data "aws_eks_cluster" "cluster" {
  name = "${module.eks.cluster_id}"
}

data "aws_eks_cluster_auth" "cluster" {
  name = "${module.eks.cluster_id}"
}
provider "kubernetes" {
  host                   = "${data.aws_eks_cluster.cluster.endpoint}"
  cluster_ca_certificate = "${base64decode(data.aws_eks_cluster.cluster.certificate_authority.0.data)}"
  token                  = "${data.aws_eks_cluster_auth.cluster.token}"
  load_config_file       = false
  version                = "~> 1.11"
}

module "eks" {
  source          = "terraform-aws-modules/eks/aws"
  cluster_name    = "${var.cluster_name}"
  cluster_version = "${var.kubernetes_version}"
  subnets         = "${concat(module.network.private_subnets, module.network.public_subnets)}"

  tags = "${
    map(
      "kubernetes.io/cluster/${var.cluster_name}", "owned",
      "KubernetesCluster", "${var.cluster_name}"
    )
  }"

  vpc_id = "${module.network.vpc_id}"

  worker_groups_launch_template = [
    {
      name                    = "spot"
      subnets                 = "${concat(slice(module.network.private_subnets, 0, length(var.availability_zones)), slice(module.network.public_subnets, 0, length(var.availability_zones)))}"
      override_instance_types = "${var.override_instance_types}"
      asg_max_size            = 1
      asg_desired_capacity    = 1
      kubelet_extra_args      = "--node-labels=node.kubernetes.io/lifecycle=spot"
      spot_allocation_strategy= "capacity-optimized"
      spot_instance_pools     = null
    },
  ]
  
  map_users    = [
    {
      userarn  = "${module.iam_user_deployer.iam_user_arn}"
      username = "${module.iam_user_deployer.iam_user_name}"
      groups   = ["system:masters"]
    },
    {
      userarn  = "${module.iam_user_admin.iam_user_arn}"
      username = "${module.iam_user_admin.iam_user_name}"
      groups   = ["global-readonly", "digit-user"]
    },
    {
      userarn  = "${module.iam_user_user.iam_user_arn}"
      username = "${module.iam_user_user.iam_user_name}"
      groups   = ["global-readonly"]
    },    
  ]
}

module "db" {
  source                        = "../modules/db/aws"
  subnet_ids                    = "${module.network.private_subnets}"
  vpc_security_group_ids        = ["${module.network.rds_db_sg_id}"]
  availability_zone             = "${element(var.availability_zones, 0)}"
  instance_class                = "db.t3.medium"
  engine_version                = "11.5"
  storage_type                  = "gp2"
  storage_gb                    = "100"
  backup_retention_days         = "7"
  administrator_login           = "egovdev"
  administrator_login_password  = "${var.db_password}"
  db_name                       = "${var.cluster_name}-db"
  environment                   = "${var.cluster_name}"
}

module "es-master" {

  source = "../modules/storage/aws"
  storage_count = 3
  environment = "${var.cluster_name}"
  disk_prefix = "es-master"
  availability_zones = "${var.availability_zones}"
  storage_sku = "gp2"
  disk_size_gb = "2"
  
}
module "es-data-v1" {

  source = "../modules/storage/aws"
  storage_count = 3
  environment = "${var.cluster_name}"
  disk_prefix = "es-data-v1"
  availability_zones = "${var.availability_zones}"
  storage_sku = "gp2"
  disk_size_gb = "25"
  
}

module "zookeeper" {

  source = "../modules/storage/aws"
  storage_count = 3
  environment = "${var.cluster_name}"
  disk_prefix = "zookeeper"
  availability_zones = "${var.availability_zones}"
  storage_sku = "gp2"
  disk_size_gb = "2"
  
}

module "kafka" {

  source = "../modules/storage/aws"
  storage_count = 3
  environment = "${var.cluster_name}"
  disk_prefix = "kafka"
  availability_zones = "${var.availability_zones}"
  storage_sku = "gp2"
  disk_size_gb = "50"
  
}

module "zookeeper-ifix" {

  source = "../modules/storage/aws"
  storage_count = 3
  environment = "${var.cluster_name}"
  disk_prefix = "zookeeper-ifix"
  availability_zones = "${var.availability_zones}"
  storage_sku = "gp2"
  disk_size_gb = "2"
  
}

module "kafka-ifix" {

  source = "../modules/storage/aws"
  storage_count = 3
  environment = "${var.cluster_name}"
  disk_prefix = "kafka-ifix"
  availability_zones = "${var.availability_zones}"
  storage_sku = "gp2"
  disk_size_gb = "50"
  
}

module "node-group" {  
  for_each = toset(["ifix-dev", "mgramseva"])
  source = "../modules/node-pool/aws"

  cluster_name        = "${var.cluster_name}"
  node_group_name     = "${each.key}-ng"
  kubernetes_version  = "${var.kubernetes_version}"
  security_groups     =  ["${module.network.worker_nodes_sg_id}"]
  subnet              = "${concat(slice(module.network.private_subnets, 0, length(var.node_pool_zone)))}"
  node_group_max_size = 1
  node_group_desired_size = 1
}  


```

## Custom Variables/Configurations <a href="#set-up-an-environment" id="set-up-an-environment"></a>

Define your configurations in **variables.tf.** Provide the environment-specific cloud requirements and use the same terraform template to customize the configurations.

```
├── sample-eks
│   ├── main.tf 
│   ├── outputs.tf
│   ├── providers.tf
│   ├── remote-state
│   │   └── main.tf
│   └── variables.tf

```

The values given below must be mentioned in the following files. The blank ones will be prompted for inputs while execution.

**​**[**variables.tf**](https://github.com/egovernments/DIGIT-DevOps/blob/release/infra-as-code/terraform/sample-aws/variables.tf) ​

```
## Add Cluster Name
variable "cluster_name" {
  default = "<Desired Cluster name>"  #eg: my-digit-eks
}

## Add vpc_cidr_block
variable "vpc_cidr_block" {
  default = "CIDR" 
}

# If you want prod grade N/W, you can define HA, DRS with multi zone
variable "network_availability_zones" {  
  default = ["ap-south-1b", "ap-south-1a"]
}

# Which zone, it matters
variable "availability_zones" {
  default = ["ap-south-1b"]
}

variable "node_pool_zone" {
 default = "ap-south-1a"  
}

variable "kubernetes_version" {
  default = "1.18"
}

# instance type for your worker nodes like r5a.large is 8 vCPU and 16GB RAM
variable "instance_type" {
  default = "r5a.large"
}

# spot instance configuration
variable "override_instance_types" {
  default = ["r5a.large", "r5ad.large", "r5d.large", "t3a.xlarge"] 
}

# number of machines as per estimate
variable "number_of_worker_nodes" {
  default = "1"
}

##Add ssh key in case you want to ssh to nodes
variable "ssh_key_name" {
  default = "ssh key name"
}

# terraform users ssh public key, you need to one for you, refer below to create yours
variable "iam_keybase_user" {
  default = "keybase:egovterraform"
}

# will be prompted to provide during the execution
variable "db_password" {}

```

{% hint style="info" %}
**Important: Create your own key base key before you run the terraform**&#x20;
{% endhint %}

​Use the URL [https://keybase.io/](https://keybase.io/) to [create your own PGP key](https://pgpkeygen.com/). This creates both public and private keys on your machine. Upload the public key into the [keybase](https://keybase.io/) account that you have just created, give a name to it and ensure that you mention that in your terraform. This allows the encryption of all sensitive information.

* Example - the keybase user (in eGov case is "_egovterraform_") needs to be created and has to be uploaded the public key here - [https://keybase.io/egovterraform/pgp\_keys.asc](https://keybase.io/egovterraform/pgp\_keys.asc)​
* you can use this [portal](https://8gwifi.org/pgpencdec.jsp) to decrypt your secret key. To decrypt PGP Message, upload the PGP Message, PGP Private Key and the Passphrase.

## Run Terraform <a href="#run-terraform" id="run-terraform"></a>

Now that we know what the terraform script does, the resources graph that it provisions and what custom values should be given with respect to your env.

Let's begin to run the Terraform scripts to provision infra required to Deploy DIGIT on AWS.

1. First CD into the following directory and run the following command 1-by-1 and watch the output closely.

```
cd iFix-DevOps/infra-as-code/terraform/sample-eks/remote-state 
terraform init
terraform plan
terraform apply


cd iFix-DevOps/infra-as-code/terraform/sample-eks 
terraform init
terraform plan
terraform apply
```

&#x20;Upon Successful execution following resources get created which can be verified by the command "terraform output"

* **s3 bucket:** to store terraform state.
* **Network:** VPC, security groups.
* **IAM users auth:** using the key base to create admin, deployer and the user. Use this URL [https://keybase.io/](https://keybase.io/) to [create your own PGP key](https://pgpkeygen.com/), this will create both public and private keys in your machine. Upload the public key into the [keybase](https://keybase.io/) account that you have just created, give a name to it and ensure that you mention that in your terraform. This allows for encrypting all sensitive information.
  * Example: keybase user (in eGov case is "_egovterraform_") needs to be created and has to be uploaded the public key here - [https://keybase.io/egovterraform/pgp\_keys.asc](https://keybase.io/egovterraform/pgp\_keys.asc)​
  * you can use this [portal](https://8gwifi.org/pgpencdec.jsp) to decrypt your secret key. To decrypt PGP Message, Upload the PGP Message, PGP Private Key and Passphrase.
* **EKS cluster:** with master(s) & worker node(s).
* **Storage(s):** for es-master, es-data-v1, es-master-infra, es-data-infra-v1, zookeeper, kafka, kafka-infra.

2\. Use this link to [get the kubeconfig from EKS](https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html) to get the kubeconfig file and be able to connect to the cluster from your local machine so that you should be able to deploy DIGIT services to the cluster.

```
aws sts get-caller-identity

# Run the below command and give the respective region-code and the cluster name
aws eks --region <region-code> update-kubeconfig --name <cluster_name>
```

3\. Verify that you are able to connect to the cluster by running the following command

```
kubectl config use-context <your cluster name>

kubectl get nodes

NAME                                             STATUS AGE   VERSION               OS-Image           
ip-192-168-xx-1.ap-south-1.compute.internal   Ready  45d   v1.15.10-eks-bac369   Amazon Linux 2   
ip-192-168-xx-2.ap-south-1.compute.internal   Ready  45d   v1.15.10-eks-bac369   Amazon Linux 2   
ip-192-168-xx-3.ap-south-1.compute.internal   Ready  45d   v1.15.10-eks-bac369   Amazon Linux 2   
ip-192-168-xx-4.ap-south-1.compute.internal   Ready  45d   v1.15.10-eks-bac369   Amazon Linux 2 
```

Whola! All set and now you can go with [Deploy Product](./#v-1-choose-the-cloud)..

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
