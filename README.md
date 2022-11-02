# two-tier
Deploying a two tier application on EKS Cluster, using Terraform

Terraform scripts to Provision AWS EKS
Steps to be followed:
1.	Create an IAM (Identity Access Management) user in AWS and add user to the user_group
•	Sign in into AWS console with your crendentials
•	IAM -> Add user -> name -> add to Group -> add tags -> ok and save.
•	After adding user ,Download new_user_credentials.csv file .
•	Go to the file location and copy the credentials
•	Open the terminal

$ cd Downloads/
$ aws configure --profile <profile name>
$ AWS Access Key ID : <paste from the csv file>
$ AWS Secret  Access Key: <paste from the csv file>
$ Default region name: us-east-1
$ Default output format: json

 
i
2.	Create the following Terraform Scripts:

•	provider.tf
•	vpc.tf
•	internet-gateway.tf
•	subnets.tf
•	eips.tf
•	nat-gateways,tf
•	route-tables.tf
•	route-table-association.tf
•	eks.tf
•	eks-nodegroup.tf

3.	Please find below url of my Github Repository for the Source code , where you can find all the Terraform Scripts as mentioned above.

https://github.com/akshaykumart/two-tier.git

4.	Go to the Terminal :

•	$ cd Terraform                             //Location where your Terraform files are located in local
•	$ terraform version                    //validate the terraform version
•	$ aws –version                            // Validate the AWS version
•	$ terraform init                          // Initialize the terraform Environment
•	$ terraform plan
•	$ terraform apply 

5.	Validations:

•	Login to AWS console and check whether the following things are created or not.

 
	Validate own VPC  created as per the Terraform script as shown above
 

	Validate IGW (Internet Gate Way) created as per the Terraform script as shown above
 
	Validate Subnets created as per the Terraform script as shown above.
 

	Validate Elastic IP’s created as per the Terraform Script as shown above.
 

	Validate NAT Gateways created as per the Terraform Script as shown above. 
 
	Validate the Routing Tables as per the Terraform script as shown above.

 

	Validate the EKS Cluster as per the Terraform Script as shown above.
Deploying a Two Tier Application on EKS Cluster
Steps to be followed:
I.	Install AWS CLI:

•	$ sudo apt-get update                                  
•	$ sudo apt install python3-pip -y           
•	$ sudo apt install awscli -y
•	$ aws configure
access key id: <provide your IAM user access key>
secret key id: <provide your IAM user secret key>
region: <region of aws resources>
format: <file format>

II.	Install AWS Authenticator :

•	$ curl -Lo aws-iam-authenticator https://github.com/kubernetes-sigs/aws-iam-authenticator/releases/download/v0.5.9/aws-iam-authenticator_0.5.9_linux_amd64
•	$ chmod +x ./aws-iam-authenticator
•	$ mkdir -p $HOME/bin && cp ./aws-iam-authenticator $HOME/bin/aws-iam-authenticator && export PATH=$PATH:$HOME/bin

III.	Install Kubectl to communicate with EKS Cluster :

•	$ curl -o kubectl https://s3.us-west-2.amazonaws.com/amazon-eks/1.23.7/2022-06-29/bin/linux/amd64/kubectl
•	$ chmod +x ./kubectl
•	$ mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$PATH:$HOME/bin

IV.	To communicate with EKS cluster :

•	$ aws eks --region <region>  update-kubeconfig --name <EKS Cluster name>
[ In region, mention your region where eks is created ]
[ In name , mention your EKS Cluster name ]
•	$ more /home/ubuntu/.kube/config      
•	$ export KUBECONFIG=~/.kube/config
•	$ kubectl get svc         //verification

V.	Deploying a Wordpress and Mysql tier on to EKS Cluster :

•	Create  a docker compose file called docker-compose.yml

https://github.com/akshaykumart/two-tier/blob/main/docker-compose.yml

[ Refer the above  Github Repository for the scripts and code]

$ docker-compose up –d                                  //creating an image from script
$ docker ps                                                         //validate the image created
$ docker login                                                    //docker hub login credentials
    username : <provide your dockerhub  account username>
    Password: <provide your dockerhub account password>
$ docker tag <image> <username/repo>:tag         //tagging a image to  username
$ docker push <username/repo>:tag                     pushing image to dockerhub

 

•	Create a deployment file and service file for wordpress app called deployment1.yml

https://github.com/akshaykumart/two-tier/blob/main/deployment1.yml

[ Refer the above  Github Repository for the scripts and code]

$ kubectl apply -f deployment1.yml

•	Create a deployment file and service file for database called deployment2.yml
                          
 https://github.com/akshaykumart/two-tier/blob/main/deployment2.yml

[ Refer the above  Github Repository for the scripts and code]

$ kubectl apply -f deployment2.yml

•	Verify that the deployments are created or not 

$ kubectl get deployments
$ kubectl get svc
$ kubectl get nodes
$ kubectl get pods
 

•	Access the application using external ip from service loadbalancer :

<External Ip from svc>:<port>
                                 
















                    



                  

