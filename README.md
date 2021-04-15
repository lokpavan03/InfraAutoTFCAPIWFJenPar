# Azure Infrastructure Automation with Jenkins Active Choices using Terraform Cloud API driven Workflow

<span style="color:black;">Contents</span>
- [GitHub Setup](#GitHub-Setup)
- [Terraform Cloud setup](#Terraform-Cloud-setup)
- [Terraform Scripts](#Terraform-Scripts)
- [Azure Key Vault Secret](#Azure-Key-Vault-Secret)
- [Azure Key Vault Jenkins Integration](#Azure-Key-Vault-Jenkins-Configuration)
- [Jenkins Pipeline](#Jenkins-Pipeline)
- [Azure Resources Validation](#Azure-Resources-Validation)

## _**GitHub Setup**_

1. Create a GitHub account use the following URL **[GitHubJoin](https://github.com/join)** if account doesn't exists.
2. Once the GitHub account created login to the GitHub portal with Username and Password.
3. Create a Repository.

![GitHub](https://github.com/lokpavan03/terraformgitaction/blob/main/gifs/github.gif?raw=true)

4. Upload the terraform scripts, Jenkinsfile and API driven workflow shell script to the GitHub repository.

![API Script](https://github.com/lokpavan03/lokpavan03/blob/gh-pages/JenkinsTFCAPIWF/JenkinsTFCAPIWF/APIdrivenWF.gif?raw=true)

## _**Terraform Cloud setup**_
1. Create a Terraform Cloud account use the following URL **[TerraformCloud](https://www.terraform.io/cloud)** if account doesn't exists.
2. Once the Terraform Cloud account created login to the Terraform Cloud portal with Username and Password.
3. Create an organization if you are new to Terraform cloud or use the existing organization.
4. Create a workspace while creating it choose API_driven workflow environment type and provide the workspace name.

![Terraform_Cloud](https://github.com/lokpavan03/InfraAutoJenkinsTFCloud/blob/master/jpgs/TerraformWorkspace.gif)


6. Setup API_TOKEN for GitHub to Terraform Cloud connection setup
7. Go to workspace -> User Settings -> Under the User options right top corner -> Tokens -> Create an API Token and name it -> Copy the Token.
8. Save the token as TF_API_TOKEN in GitHub Secrets and provide the secret under the terraform configuration provider in **main.tf** file.
9. Service Principal login needs the following variables and get the values from the Azure App

          * subscription_id
          * client_id
          * client_secret
          * tenant_id

![Terraform_Token](https://github.com/lokpavan03/InfraAutoJenkinsTFCloud/blob/master/jpgs/TerraformToken.gif)

## _**Terraform Scripts**_
1. Create the Scripts as per the Azure resources requirement.
2. In Terraform **main.tf** is the main file it contains the Terraform Cloud Configuration block, Azure resource provider block and resoures block.
3. In Terraform **variables.tf** contains all the variable declaration information.

![Terraform_Scripts](https://github.com/lokpavan03/lokpavan03/blob/gh-pages/JenkinsTFCAPIWF/JenkinsTFCAPIWF/Terraform_scripts.gif?raw=true)

##_**Azure Key Vault Secret**_
1. Login to the Azure Portal **[AzurePortal](https://portal.azure.com)** with your credentials
2. Go to the Key Vault if exists otherwise create a key vault.
3. Store the Terraform cloud **APITOKEN** under the secrets.

![Azure Key Vault](https://github.com/lokpavan03/lokpavan03/blob/gh-pages/JenkinsTFCAPIWF/JenkinsTFCAPIWF/AzureKeyVault.gif?raw=true)

##_**Azure Key Vault Jenkins Integration**_
1. Go to the Jenkins dashboard.
2. click on Manage Jenkins->Manage Plugins->Under available Plugine search for **Azure Key Vault** plugin and install it.
3. Jenkins communicate the Azure Key Vault with Service Principal.
4. Go to Manage Credentials under Manage Jenkins -> choose the Jenkins under the credentials.
5. Select Global Credentials under system -> Add Credentials
6. Under the kind choose **Microsoft Azure Service Principal** and provide the Client ID, Tenant ID, Client Secret and Subscription ID details and save it.
7. We call the Key Vault with Key Vault URL using Service Principal.

![Key Vault Integration](https://github.com/lokpavan03/lokpavan03/blob/gh-pages/JenkinsTFCAPIWF/JenkinsTFCAPIWF/KeyVaultConfig.gif?raw=true)

## _**Jenkins Pipeline**_
1. Create a New Item in the Jenkins dashboard and choose the pipeline job and provide name for it.

![Jenkins Pipeline](https://github.com/lokpavan03/lokpavan03/blob/gh-pages/JenkinsTFCAPIWF/JenkinsTFCAPIWF/JenkinsPipeline.gif?raw=true)

3. Generate the Jenkins pipeline script using syntax generator.
4. Once script is reade, save the file as Jenkinsfile and store it in GitHub repository.
5. Run the Jenkinsfile from the pipeline through SCM.

![Jenkinsfile](https://github.com/lokpavan03/lokpavan03/blob/gh-pages/JenkinsTFCAPIWF/JenkinsTFCAPIWF/JenkinsFile.gif?raw=true)

6. Run the Jenkins Pipeline Job with Build Parameters and provide the necessary inputs.

![JenkinsPipelineRun](https://github.com/lokpavan03/lokpavan03/blob/gh-pages/JenkinsTFCAPIWF/JenkinsTFCAPIWF/RunningPipeline.gif?raw=true)

7. Once Pipeline completed successfully. 
8. Login to the Terraform Cloud account and check the run under the requested Workspace.
9. Once **PLAN** is completed successfully. 
10. Confirm the **APPLY** to run.

![Terraform Apply](https://github.com/lokpavan03/lokpavan03/blob/gh-pages/JenkinsTFCAPIWF/JenkinsTFCAPIWF/TerraformValidation.gif?raw=true)

## _**Azure Resource Validation**_
1. Login to the Azure Portal **[AzurePortal](https://portal.azure.com)** with your credentials
2. Go to resouce group and check for created resources.
3. Validate whether the resources created or not.

![Azure Resources Validation](https://github.com/lokpavan03/lokpavan03/blob/gh-pages/JenkinsTFCAPIWF/JenkinsTFCAPIWF/Validation.gif?raw=true)

4. Login to the VM with the Parameters and Validate.

![VMValidation](https://github.com/lokpavan03/lokpavan03/blob/gh-pages/JenkinsTFCAPIWF/JenkinsTFCAPIWF/server_validation.gif?raw=true)

Thanks,
Lok
