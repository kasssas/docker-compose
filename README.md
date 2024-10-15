# Employee & Project Management App

A web application built with Node.js, React.js, and MongoDB for managing developers and projects. The app allows administrators to add developers, create projects, and assign developers to specific projects.

## Table of Contents

- [Employee & Project Management App](#employee--project-management-app)
  - [Features](#features)
  - [Prerequisites](#prerequisites)
  - [Development](#development)
  - [Usage](#usage)
- [Docker](#docker)
  - [Installation](#installation)
  - [Build Dockerfile](#build-dockerfile)
  - [Run Dockerfile](#run-dockerfile)
  - [Pull my image locally](#pull-my-image-locally)
  - [Docker Compose](#docker-compose)
    - [Activate Docker-Compose](#activate-docker-compose)
  - [Push image to DockerHub](#push-image-to-dockerhub)


## Features

- Add and manage employee (developer) records.
- Create and manage projects.
- Assign developers to projects.
- User authentication and authorization for managing records.
- Frontend built with React.js, backend with Node.js (Express), and MongoDB for data storage.
- Automated CI/CD pipeline for testing, building, pushing to DockerHub and Deploying on AWS.

## Prerequisites

Ensure you have the following installed:

1. **Node.js (v14+)**
2. **npm (Node Package Manager)**
3. **MongoDB**
4. **Docker**
5. **Jenkins**
6. **AWS CLI**
7. **Docker-compose**
8. **Terraform**
9. **Ansible**
10. **minikube and kubectl**


## Development

Instructions for deploying the application:

1. Ensure all prerequisites are installed.
2. Clone the repository and navigate to the project directory.
3. start the MongoDB
3. Install backend and frontend dependencies.
4. Start both the backend and frontend servers.
5. Open the app at `localhost:3000`.

```bash
# Clone the repository
git clone https://github.com/kasssas/DEPI_Final_Project

#If MongoDB is running locally, ensure it's started with the default port:
mongod
cd source_code

# Backend setup
cd backend/
npm install
npm run dev

# Frontend setup
cd .frontend/
npm install
npm start
```
## Usage


- Open App `localhost:3000`.

![img_1](https://github.com/user-attachments/assets/ee0eb0c6-c053-49e2-858c-55622a939372)

![img_2](https://github.com/user-attachments/assets/d6f42871-c0c6-4d8f-93b3-4371b8ec15ca)



## Installation

Ensure Docker is installed on your system. Follow the official [Docker Installation Guide](https://docs.docker.com/engine/install/).


## Build Dockerfile

- frontend image
```bash
    docker build -t < dockerhubacc/frontend_image_name > .
```
![img_3](https://github.com/user-attachments/assets/062af6a7-27e3-4d4a-8bd2-90f03ebac129)

- backendend image
```bash
    docker build -t < dockerhubacc/backend_image_name > .
```
![img_4](https://github.com/user-attachments/assets/e146e873-1594-416c-b61d-a63a99e6aa09)


## Run Dockerfile
```bash
    docker run -p 3000:3000 < dockerhubacc/frontend_image_name >
    docker run -p 8000:8000 < dockerhubacc/backend_image_name >
```

## push my image to DockerHub

```bash
   docker login -u <your-username> -p <your-password>
   docker push  dockerhubacc/frontend_image_name
   docker push  dockerhubacc/backend_image_name
```



## Docker Compose
### Activation Docker-Compose

```bash
    docker compose up -d
```
![img_5](https://github.com/user-attachments/assets/da152a7f-637c-41c9-8561-af3fefa5f317)

- Access Services `localhost:3000`.

![img_1](https://github.com/user-attachments/assets/ee0eb0c6-c053-49e2-858c-55622a939372)

![img_2](https://github.com/user-attachments/assets/d6f42871-c0c6-4d8f-93b3-4371b8ec15ca)
![loc](https://github.com/user-attachments/assets/dc070cea-4a2f-4ca2-ad23-1fff3e288bc0)


# Kubernetes Deployment for My Application

![kuberenetes](https://github.com/user-attachments/assets/0a763809-e01b-4854-821f-1498be63cc75)

- Kubernetes manifests to deploy and manage the application.

## Table of Contents

- [Kubernetes Deployment for My Application](#kubernetes-deployment-for-my-application)
  - [Table of Contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
  - [Kubernetes Manifests](#kubernetes-manifests)
  - [Deployment](#deployment)
  - [Usage](#usage)
  - [ingress](#ingress)
  - [Cleanup](#cleanup)

## Prerequisites

- **minikube** 
```bash
(minikube version: v1.33.1
commit: 5883c09216182566a63dff4c326a6fc9ed2982ff) 
```
- **kubectl** 
```bash
Client Version: v1.31.0
Kustomize Version: v5.4.2
Server Version: v1.30.0
```
- **Docker** (for building images)

## Kubernetes Manifests

- **Namespace**: Defines a namespace for isolating resources.
- **LimitRange**: Sets resource limits for the namespace.
- **Deployment**: Manages the deployment of the application.
- **Service**: Exposes the application within the cluster.
- **Pod**: Defines the individual pods (if needed).

## Deployment

1. **Create the deployments, services, PVC**:
    ```bash
    kubectl apply -f kubernetes
    ```
![apply](https://github.com/user-attachments/assets/2598c9d7-e223-4b6b-bce4-b9a099f4c570)


## Usage

then the application will be acess via the service 
```bash
minikube service frontend 
```

![service](https://github.com/user-attachments/assets/c6479df9-efac-49d3-81ac-3a4359ec193a)


## Cleanup

To delete all the resources created:

```bash
kubectl delete all --all
```

# Terraform AWS Configuration

![terraform](https://github.com/user-attachments/assets/25f7ffe6-2f75-46b7-a1ec-8a5ba2ca0016)

This Terraform configuration build infrastructure to deploy the app on aws and access it throw DNS of loadbalancer 

## Table of Contents

- [Terraform AWS Configuration](#terraform-aws-configuration)
  - [Key Components](#key-components)
  - [Resources After Apply Terraform](#Resources-After-Apply-Terraform)
  - [Access Application](#access-application)


### Key Components

- **AWS VPC**:
- **subnets**:
- **AWS Security Group**: Allows All inbound traffic from anywhere.
- **EC2 Instances**: Launches 3 `t3.medium` instances with Ubuntu 24.04 LTS.
- **AMI**: configuared with all requirements to launch the app
- **Application loadbalancer**: to distributes and balances the incoming traffic

```bash
cd terraform
terraform init
terraform plan
terraform apply
```
![terraform1](https://github.com/user-attachments/assets/5f78c3cc-9c08-47d6-bf8f-bcada684f212)
![terraform2](https://github.com/user-attachments/assets/2be06e24-131b-46dc-b52a-7ff54e2cf231)
![terraform3](https://github.com/user-attachments/assets/4439ec09-5495-42ca-98fd-0dd68e94a77b)
![terraform4](https://github.com/user-attachments/assets/6fff8379-efbe-49c9-a7d1-29acaa17c8a5)
After finishing from AWS 
```bash
terraform destory
```
### Resources After Apply Terraform

![11](https://github.com/user-attachments/assets/3d97cb8f-7f51-45e2-b5b6-2690c7c7bbd3)
![12](https://github.com/user-attachments/assets/1f962856-eb8b-4e58-8d42-b04054bad84e)




### Access Application
![aws](https://github.com/user-attachments/assets/f97cd70f-ec01-48c2-a798-c6684229af91)

________

# Ansible 

![ansible](https://github.com/user-attachments/assets/e266c548-f6e0-4313-bd1d-acab5f916ca8)

Using Ansible to configure an EC2 instance as a Jenkins slave to automate CI/CD processes. By leveraging Ansible's playbooks installed necessary dependencies like docker, docker-compose, Git, AWS Cli and terraform. Afterward, I connected the EC2 instance to the Jenkins master, enabling it to execute the Jenkinsfile for automated builds and deployments.

## Table of Contents

- [Ansible](#ansible)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Running the Playbook](#running-the-playbook)


## Prerequisites

Before you can run the playbook, ensure you have the following:

- Pipx
- Dependencies

## Installation
[Install Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-and-upgrading-ansible-with-pipx)

1. **Install Ansible** on your control machine. You can install it using:
    ```bash
    sudo apt update
    pipx install --include-deps ansible
    pipx install ansible-core
    pipx install ansible-core==2.12.3
    ```

2. **Access your AWS instances** via SSH. Make sure you have the `labsuser.pem` key file and it's properly configured:
    ```bash
    cd Downloads/
    sudo chmod 400 /home/mostafa/.ssh/private-key.pem
    ssh -i /home/mostafa/.ssh/private-key.pem ec2-user@<public_ip_or_dns_of_instance>
    ```

## Running the Playbook

To run the playbook, execute the following command:
```bash
cd ansible/
ansible-playbook -i hosts.ini ec2_setup.yml
```


## Jenkinks

![Jenkins](https://github.com/user-attachments/assets/7fed81a8-0043-4174-b1c1-27552f672a35)

### Jenkins Pipeline

This Jenkins pipeline automates process of cloning the code, installing dependencies, running tests, and building a Docker image, pushing it to dockerhub and update the infrastructure on aws.

## Jenkins installation
[Install Jenkins on Linux](https://www.jenkins.io/doc/book/installing/linux)

- Get the passkey of Jenkins server to login from default port `8080`

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

## Pipeline Stages

1. **Requirements And Test**
   - Set up virtual environment`
   - Run tests 

2. **Docker Building**
   - Build Docker image tagged as `image`
  
3. **Login in DockerHub**
4.  **Push image autamatincly**
5. **update the infrastructure on AWS** 
## Usage

- Add the provided `Jenkinsfile` to your repository.
- Configure a Jenkins pipeline job to use this `Jenkinsfile`.
- Ensure Jenkins has Docker, aws cli and terraform installed on its agents.
- Add necessary credentials to the Jenkins pipeline

1. **Credentials**

![img_7](https://github.com/user-attachments/assets/72fd19e0-11f8-4017-892e-07937c617f09)

![img_8](https://github.com/user-attachments/assets/c4f9756f-358b-49d8-ac4e-e9dbf8a82dde)

![img_9](https://github.com/user-attachments/assets/72d3025c-d307-4423-875f-e65ea35d7652)

# 2. **Build**

![img_10](https://github.com/user-attachments/assets/1de855f3-9093-418f-847e-1e04470d799a)


![imgg_11](https://github.com/user-attachments/assets/895cc976-cc3e-4daf-a617-8026a182c227)

![img_12](https://github.com/user-attachments/assets/f634b008-7838-41f0-ad5f-5d7a7bcb6f42)