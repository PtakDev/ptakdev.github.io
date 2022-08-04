---
title: Updating State in Terraform Enterprise
date: 2022-08-04 08:00:00 +0100
categories: [Guides, Terraform]
tags: [terraform, terraform enterprise, tfe, tfstate]     # TAG names should always be lowercase
---

# Updating State in Terraform Enterprise

## Step 1. Login to your organization terraform
If you are already looged in go to the next step.

```shell
terraform login <HOSTNAME>
```
After executing this command, the explorer should open and it will allow you to create a token. You need to copy the token and paste it in shell. 

> Save the token somwhere safe, as you wont be able to see it again.
{: .prompt-tip } 

## Step 2. Crete new working directory
Crete new working directory and inside this directory create new file called 'provider.tf'.
   
## Step 3. Update 'provider.tf' file 
Inside this file you will have to specify the hostname, name of your organization and workspace. 

```
terraform {
  backend "remote" {
    hostname = "<HOSTNAME>"
    organization = "<ORGANIZATION_NAME>"
    workspaces {
      name = "<WORKSPACE_NAME>"
    }
  }
}
```
{: file="provider.tf" }

## Step 4. Initialize terraform
After saving the file, we need to open terminal and navigate to our working directory. When we are in it, we need to init terraform.

```shell
terraform init
```

## Step 5. Copy over .tfstate file
Once this process is finished, we need to move .tfstate file to our working directory.

## Step 6. Update the state
When we have .tfstate file in our working directory, we can push the file using below command.

```shell
terraform state push <FILE_NAME>.tfstate
```

## Step 7. Verify the change
Open your TFE and navigate to Organization &rarr; Workspaces &rarr; Workspace &rarr; States. Here you should be able to se new state.

> The name of the state should start with `New state #.....`.
{: .prompt-info }

Now, you should be able run `Plan` without any probles. 