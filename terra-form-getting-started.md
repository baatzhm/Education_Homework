# Getting Started with Terraform

Terraform is an open-source infrastructure as code software tool that provides a consistent CLI workflow to manage hundreds of cloud services. Terraform codifies cloud APIs into declarative configuration files. Get Started here.

## Prerequisites

- Terraform **version 1.1.7** or later
- [Kubernetes comand-line interface (CLI)](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [Minikube](https://minikube.sigs.k8s.io)

## Install Terraform
The first step to getting started with Terraform is to get it installed. 

To install Terraform, find the [appropriate package](https://www.terraform.io/downloads.html) for your platform, machine or environment and download it. Terraform is packaged as a zip archive.

After downloading Terraform, unzip the package. Terraform runs as a single binary named `terraform`.

Finally, make sure that the `terraform` binary is available on your`PATH`. This process will vary depending on your operating system.

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

Paste the following lines into the file.

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

Initialize Terraform with the `terraform init` command. The AWS provider will be installed. 

```shell
$ terraform init
```

Check that your configuration is error-free. If your configuration is valid, Terraform will return a success message.

Provision your resource with the `terraform apply` command.

```shell
$ terraform apply
```

The command will take a few minutes to run. Once complete, a message will display indicating that the resource was created.

## Destroy Infastructure
Now that you have succesfully created infastructure with Terraform, you will use Terraform to destroy this infrastructure.

```shell
$ terraform destroy
```

Type `yes` to destroy the infrastructure. Terraform will destroy the resources you created earlier.



## Next steps
That's it! You've just created and destroyed your first infastructure with Terraform!

To learn how to create real infrastructures with your preferred cloud provider, see the [Terraform] Get Started (https://learn.hashicorp.com/terraform)  documentation.
