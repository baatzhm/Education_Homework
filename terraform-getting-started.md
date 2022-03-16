# Getting Started with Terraform

Terraform is an open-source infrastructure as code software tool that provides a consistent CLI workflow to manage hundreds of cloud services. Terraform codifies cloud APIs into declarative configuration files. This guide walks you through how to get started with Terraform, deploying and destroying nginx infrastructure inside of a Docker container.

## Prerequisites

- Ability to install Terraform on your local machine
- Working Docker installation 
- Internet connection for provider plug-ins

## Install Terraform
The first step to getting started with Terraform is to get it installed. HashiCorp distributes Terraform as a [binary package](https://www.terraform.io/downloads.html). You can also install Terraform using popular package managers. 

For more detail about installation options, see [install terraform](https://learn.hashicorp.com/tutorials/terraform/install-cli)

## Build Infrastructure
With Terraform installed, you are ready to build your first infrastructure.

We recommend creating a new directory on your local machine. Create a Terraform configuration code inside the directory.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

Next, create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

Paste the following into the file.

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}
provider "docker" {
    host = "unix:///var/run/docker.sock"
}
resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}
resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

Initialize Terraform with the `terraform init` command. 

```shell
$ terraform init
```

Check for any errors. If your configuration is valid, Terraform will return a success message.

Provision your resource with the `terraform apply` command.

```shell
$ terraform apply
```

The command will take a few minutes to run. Once complete, a message will display indicating that the resource was created. 

## Destroy Infrastructure
Now that you have succesfully created infrastructure with Terraform, you will use Terraform to destroy this infrastructure.

```shell
$ terraform destroy
```

Review the output. Type `yes` to destroy the infrastructure. Terraform will destroy the resources you created earlier.



## Next steps
That's it! You've just created and destroyed your first infastructure with Terraform.

To learn how to create real infrastructures with your preferred cloud provider, see the Terraform [Get Started](https://learn.hashicorp.com/terraform) documentation.
