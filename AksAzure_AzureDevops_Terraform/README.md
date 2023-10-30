# Provision Azure AKS Cluster using Terraform
## Step-01: Introduction

    Create SSH Keys for AKS Linux VMs
    Declare Windows Username, Passwords for Windows nodepools. 
	This needs to be done during the creation of cluster for 1st time itself if you have plans for Windows workloads on your cluster
    Understand about Datasources and Create Datasource for Azure AKS latest Version
    Create Azure Log Analytics Workspace Resource in Terraform
    Create Azure AD AKS Admins Group Resource in Terraform
    Create AKS Cluster with default nodepool
    Create AKS Cluster Output Values
    Provision Azure AKS Cluster using Terraform
    Access and Test using Azure AKS default admin --admin
    Access and Test using Azure AD User as AKS Admin

## Step-02: Create SSH Public Key for Linux VMs

## Step-03: Create 3 more Terraform Input Vairables to variables.tf

    SSH Public Key for Linux VMs
    Windows Admin username
    Windows Admin Password

## Step-04: Create a Terraform Datasource for getting latest Azure AKS Versions

    Understand Terraform Datasources concept as part of this step
    Data sources allow data to be fetched or computed for use elsewhere in Terraform configuration.
    Use of data sources allows a Terraform configuration to make use of information defined outside of Terraform, or defined by another separate Terraform configuration.
    Use Azure AKS versions datasource API to get the latest version and use it
    Data Source: azurerm_kubernetes_service_versions

## Step-05: Create Azure Log Analytics Workspace Terraform Resource

    The Azure Monitor for Containers (also known as Container Insights) feature provides performance monitoring for workloads running in the Azure Kubernetes cluster.
    We need to create Log Analytics workspace and reference its id in AKS Cluster when enabling the monitoring feature.
    Create a file 05-log-analytics-workspace.tf

## Step-06: Create Azure AD Group for AKS Admins Terraform Resource

    To enable AKS AAD Integration, we need to provide Azure AD group object id.
    We wil create a Azure Active Directory group for AKS Admins

## Step-07: Create AKS Cluster Terraform Resource

    Create a file named aks-cluster.tf
    Understand and discuss about the terraform resource named azurerm_kubernetes_cluster
    This is going to be a very big terraform template when compared to what we created so far we will do it slowly step by step.

## Step-08: Create Terraform Output Values for AKS Cluster
    Create a file named outputs.tf

## Step-09: Deploy Terraform Resources

# Initialize Terraform from the folder manifests
## Anyway our state storage is from Azure Storage we are good from any folder
terraform init

## Validate Terraform manifests
terraform validate

## Review the Terraform Plan
terraform plan

## Deploy Terraform manifests
terraform apply 

Step-10: Access Terraform created AKS cluster using AKS default admin

## Azure AKS Get Credentials with --admin
az aks get-credentials --resource-group terraform-aks-dev --name terraform-aks-dev-cluster --admin

## Get Full Cluster Information
az aks show --resource-group terraform-aks-dev --name terraform-aks-dev-cluster
az aks show --resource-group terraform-aks-dev --name terraform-aks-dev-cluster -o table

## Get AKS Cluster Information using kubectl
kubectl cluster-info

## List Kubernetes Nodes
kubectl get nodes

Step-11: Verify Resources using Azure Management Console

    Resource Group
        terraform-aks-dev
        terraform-aks-dev-nrg
    AKS Cluster & Node Pool
        Cluster: terraform-aks-dev-cluster
        AKS System Pool
    Log Analytics Workspace
    Azure AD Group
        terraform-aks-dev-cluster-administrators

Step-12: Create a User in Azure AD and Associate User to AKS Admin Group in Azure AD

    Create a user in Azure Active Directory
        User Name: (username)
        Name: (username)
        First Name: (first name)
        Last Name: (last name)
        Password: ******
        Groups: terraform-aks-prod-administrators

        Click on Create

    Login and change password
        URL: https://portal.azure.com
        Username: (your domain name)
        Old Password: *****
        New Password: *****
        Confirm Password: *****

Step-13: Access Terraform created AKS Cluster

## Azure AKS Get Credentials with --admin
az aks get-credentials --resource-group terraform-aks-dev --name terraform-aks-dev-cluster --overwrite-existing

## List Kubernetes Nodes
kubectl get nodes
URL: https://microsoft.com/devicelogin
Code: ***** (sample)
Username: (your domain name)
Password: (your password)


