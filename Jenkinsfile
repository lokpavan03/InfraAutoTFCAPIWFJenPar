pipeline {
    agent any
    environment {
        TOKEN = credentials('TFAPITOKENAD')
    }
    //Active Choice Parameters these values are input to the terraform.auto.tfvars
    parameters {
        string defaultValue: 'VM001-Jenkins', description: 'Please provide the VM Name', name: 'VirtualMachineName'
        string defaultValue: 'West Europe', description: 'Please Provide the Resource group location if you want to change', name: 'ResourceGroupLoaction'
        string defaultValue: 'TFCloudRG001', description: 'Please Provide the Resource group name if you want to change', name: 'RescourceGroupName'
        string defaultValue: 'subnet01', description: 'Please provide the Subnet Name if need change', name: 'SubNetName'
        string defaultValue: 'adminuser', description: 'Please provide the VM User Name', name: 'VMUserName'
        password defaultValue: 'Admin123', description: 'Please provide the password if you want change default', name: 'VMPassword'
    }
    stages {
        //checkout the Github code
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitCreds', url: 'https://github.com/lokpavan03/InfraAutoTFCAPIWFJenPar.git']]])
            }
        }
        //createing the terraform.auto.tfvars file from the choices parameters input
        stage('TFvarsFile') {
            steps {
                writeFile file: 'terraform.auto.tfvars', text:  """resource_group_name = "${params.RescourceGroupName}" \nresource_group_location = "${params.ResourceGroupLoaction}"\nvnet_name = "${params.VirtualNetworkName}"\nsubnet_name = "${params.SubNetName}"\nazure_virtual_machine_name = "${params.VirtualMachineName}"\nadmin_vm_username = "${params.VMUserName}"\nadmin_vm_password = "${params.VMPassword}"\n"""
            }
        }      
        //Initializing Terrraform
        stage('Terraform init') {
            steps {
                sh 'chmod +x ./APIScript.sh'
                sh './APIScript.sh ./ loktf/TestDemo'
            }
            environment {
                TOKEN = credentials('TFAPITOKENAD')
            }
        }                  
                    
    }
}
