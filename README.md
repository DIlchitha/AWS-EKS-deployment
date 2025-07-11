**﻿ AWS EKS Deployment**
AWS EKS (Elastic Kubernetes Service) is a managed Kubernetes service provided by Amazon Web Services (AWS). Kubernetes is an open-source container orchestration platform that simplifies the deployment, scaling, and management of containerized applications. With EKS, AWS takes care of the underlying infrastructure and management tasks, allowing you to focus on deploying and running your applications in a scalable and highly available manner.

**Here are the steps How to deploy nginx server in AWS EKS**

** Create a IAM User**

  -> step1: Log in to AWS Management Console 
               
  -> step2: Navigate to IAM service
               
  -> step3: Click "Users" in the left side
               
   -> step4: Click "Add user"
               
  -> step5: Enter a username (e.g., "api-user")
               
   -> step6: Select "Programmatic access" as the access type
               
  -> step7: Click "Next: Permissions"


 Create IAM rule and give access policy

 ![1 - Create IAM rules and given Access policy](https://github.com/user-attachments/assets/759cb16f-a87e-4081-9e61-4e507bc19325)


 Create IAM User

 ![2 - Created IAM user](https://github.com/user-attachments/assets/b1d64909-c25e-4681-b369-6d3742984fd0)


 Gernerate Access key and Secrete Key in IAM User

 ![3 - Generate access key and secret key for IAM user](https://github.com/user-attachments/assets/037232ef-e744-4755-9945-c556e871422a)


**Create EC2 Instance**

  -> Log in to AWS Console and navigate to EC2 service
  
  -> Configure the instance: AMI, Instance type, key pair, Allow SSH (port 22) from your IP, storsge


Lounch EC2 Instance

![4 - create EC2 User](https://github.com/user-attachments/assets/8bbf99bb-be20-4ed1-a0f0-aee4a8edcac6)


Connect EC2 in mobaxterm

![5 - Connect ec2 in mobaxterm](https://github.com/user-attachments/assets/9af073da-7599-4fda-b99f-010ee3e6efb8)



**Install latest version of AWS CLI for amazon linux**

   -> Step1: Download the AWS CLI Bundle

               curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

   -> step2:Unzip the Package

              unzip awscliv2.zip

   ->  Step3: Install AWS CLI

                sudo ./aws/install

   -> Step 4: Verify Installation
   
                aws --version

   -> Configure the aws cli (Access Key->   AKIAXCL4GZO3KVKEFDJC, secret key   -> .......................... , region ->  eu-north-1)
   

 AWS CLI Install

  ![6 - AWS CLI](https://github.com/user-attachments/assets/7a5bdb94-521d-4dab-b40b-6ad3596352fa)


AWS CLI Configure

![7 - AWS  CLI configure](https://github.com/user-attachments/assets/bcfcded0-244a-457e-a1fe-2f317044d0e6)



**Kubectl Installation**

 -> Download the kubectl Pakages step by step

    # Update your system packages
    sudo yum update -y

    # Install kubectl
    sudo curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    # Make the binary executable
    sudo chmod +x ./kubectl

    # Move to PATH
    sudo mv ./kubectl /usr/local/bin/kubectl

    # Verify installation
    kubectl version --client

        


Kubectl Instalation 

![8 - kubectl installaton](https://github.com/user-attachments/assets/9f1d12f4-28ad-408e-b89e-52237d0bef5f)



**Install EKS CTL**

 -> Step 1: Download the EKS CTL pakage

         curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp

  -> step 2 :  Move eksctl
  
         sudo mv /tmp/eksctl /usr/local/bin
 
  -> step 3:  Verify installation
    
         eksctl version

   -> Create EKS Cluster

          eksctl create cluster \
         --name my-cluster \
         --region eu-north-1 \
         --nodegroup-name standard-worker \
         --node-type t3.medium \
         --nodes 3 \
         --nodes-min 1 \
         --nodes-max 4 \
         --managed


Install EKS CTL

![9 - Install EKS CTL](https://github.com/user-attachments/assets/d3891e9a-bdc9-4ca1-a179-aede6cad8879)



Create EKS Cluster

![10 - Create EKS Cluster](https://github.com/user-attachments/assets/a5ff72c1-be89-4eee-a757-ff9e667732a9)




Nodes and Workers automatically create after cluster created

![11 - Node   workers automatically create](https://github.com/user-attachments/assets/db37afe4-873e-4c62-a08f-cc725e763781)



CLuster & Nodes create automatically

![Cluster   Node create](https://github.com/user-attachments/assets/64ee8615-86f0-44d4-83b2-c6699c61e156)



Cluster Creation

![12 - cluster creat](https://github.com/user-attachments/assets/41caa268-d269-4c0e-a36c-d465da2b7ecc)



Cluster status

![13 - Cluster status](https://github.com/user-attachments/assets/a833032a-c65e-4ff8-b6a5-da98343c2acc)


 -> Communicate with cluster
 
    ksctl get cluster

  -> enableconnect the cluster
  
      aws eks update-kubeconfig  --name my-cluster --region eu-north-1


**deployment a cluster with Git hub repository**

  -> step 1: Install the git for Virtual Machine
  
        sudo yum install -y git 

  -> Step2: Clone the gir repository 
  
        git clone https://github.com/DIlchitha/AWS-EKS-deployment.git



Git Repository Clone to the Virtual Machine

![14 - Git repositoary Clone](https://github.com/user-attachments/assets/49129748-dd43-471f-a707-f8919558a2fa)



View the Deployment.yaml & service.yaml files successfully clone or not

![16 - view the service yaml file](https://github.com/user-attachments/assets/9d6cd6f8-9103-4d44-b2ea-e8b2f02e004a)



  -> apply the Service and Deployment  file to kubecluster
  
       kubectl apply -f  nginx-svc.yaml  
       kubectl apply -f  nginx-deployment

  
Check the status of Deployment and service yaml files

![17 - check the status of service yaml and deployment yaml](https://github.com/user-attachments/assets/916592d1-616d-4bbb-8020-8dc6b322f755)



  -> get pods
  
       kubectl get pods
       
  -> get nodes
  
       kubectl get nodes



view the pods and Nodes

![18 - view the pods in load balancer](https://github.com/user-attachments/assets/5465c2e4-f748-4da9-9d79-be29c04c4ff2)



View the pods in load balencer

![18 - view the pods in load balancer](https://github.com/user-attachments/assets/d87af0a4-e2ef-4ab5-a774-99f03a46b72f)



 -> view Kubernetes application runnig on load balancer
 
     curl a8e525e858180478d914e0f7b1e8aed4-1796081403.eu-north-1.elb.amazonaws.com


Successfully application running on Load balaner DNS in browser

![20 - application running on Load balancer DNS](https://github.com/user-attachments/assets/c3cfe021-e3af-40a9-a720-bff24145e701)



Successfully application running on Load balaner DNS in VIrtual Server

![20 - successfully run on application use load balencer DNS](https://github.com/user-attachments/assets/fdcd6a43-6ce8-489b-b6f3-30300e0429d8)


                          
