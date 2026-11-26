# Netflix-Clone-CI-CD-Pipeline-DevSecOps

## Project Overview

This project demonstrates the implementation of an end-to-end **CI/CD DevSecOps pipeline** for deploying a Netflix Clone application using AWS, Jenkins, SonarQube, Trivy, Docker, Kubernetes and monitoring tools.

The main objective is to automate the application deployment process by integrating continuous integration, security scanning, containerization, infrastructure provisioning, Kubernetes deployment and monitoring.

The project uses Jenkins Declarative Pipeline to automate the complete workflow, from source code checkout to application deployment.

## Architecture & Workflow
<img width="1536" height="1024" alt="Architecture-latest" src="https://github.com/user-attachments/assets/4e97502a-d1ac-45cb-bf91-9a79ca9733d1" />

**Project Flow:**

Developer → GitHub → Jenkins → SonarQube → Security Scanning → Docker Build → Docker Hub → AWS EKS → Kubernetes → Prometheus → Grafana

### Pipeline Architecture

1. **Source Code Management**
   - GitHub repository stores the Netflix Clone application.
   - GitHub Webhook triggers the Jenkins pipeline when code is pushed.

2. **Continuous Integration – Jenkins**
   - Jenkins manages the complete CI/CD workflow.
   - Checks out the source code.
   - Installs application dependencies.
   - Executes automated pipeline stages.

3. **Code Quality – SonarQube**
   - Performs static code analysis.
   - Identifies code quality issues.
   - Integrates with Jenkins Quality Gate.

4. **Security Scanning**
   - Trivy performs filesystem vulnerability scanning.
   - Trivy scans the Docker image.
   - NPM is used to install application dependencies.
   - OWASP Dependency Check plugin is configured in Jenkins.

5. **Docker Containerization**
   - Builds the Netflix application Docker image.
   - Tags the image.
   - Pushes the image to Docker Hub.
   - Scans the Docker image using Trivy.

6. **Infrastructure Provisioning – Terraform**
   - Provisions AWS EKS infrastructure.
   - Uses Terraform to manage infrastructure.
   - Stores Terraform state in an S3 bucket.

7. **Kubernetes Deployment**
   - Connects Jenkins to the AWS EKS cluster.
   - Deploys the application using Kubernetes deployment and service manifests.
   - Exposes the application through a Kubernetes service.

8. **Monitoring and Observability**
   - Prometheus collects system and Jenkins metrics.
   - Node Exporter exposes server-level metrics.
   - Grafana visualizes collected metrics through dashboards.

9. **Email Notifications**
   - Jenkins Email Extension Plugin sends build notifications.
   - Build logs and Trivy scan reports can be attached to notifications.

## Tools & Technologies

| Category | Tools |
|---|---|
| Cloud Platform | AWS |
| Operating System | Ubuntu 24.04 |
| Source Code Management | Git, GitHub |
| CI/CD | Jenkins |
| Infrastructure as Code | Terraform |
| Code Quality | SonarQube |
| Security Scanning | Trivy, NPM Audit |
| Dependency Security | OWASP Dependency Check |
| Containerization | Docker |
| Container Registry | Docker Hub |
| Container Orchestration | Kubernetes |
| Managed Kubernetes | AWS EKS |
| Monitoring | Prometheus |
| Visualization | Grafana |
| Metrics Exporter | Node Exporter |
| Notifications | Jenkins Email Extension |
| Application | Netflix Clone |

## AWS Infrastructure

### Jenkins Server

- EC2 Instance: Ubuntu 24.04
- Instance Type: t2.large
- Storage: 50 GB
- IAM Role attached to EC2.
- Jenkins installed and configured.
- Docker and Trivy installed.
- Terraform, AWS CLI and kubectl installed.
- SonarQube deployed using Docker.

### Monitoring Server

A separate Ubuntu EC2 instance is used for monitoring.

Installed components:

- Prometheus
- Grafana
- Node Exporter

### AWS EKS

Terraform is used to provision the Kubernetes infrastructure.

The Jenkins pipeline supports two Terraform operations:

- Apply – Create infrastructure.
- Destroy – Remove infrastructure.

Terraform state is stored in a private S3 bucket.

## Jenkins Pipeline Stages

The Jenkins Declarative Pipeline automates the following stages:

| Stage | Description |
|---|---|
| Clean Workspace | Removes previous build files |
| Git Checkout | Downloads application source code |
| SonarQube Analysis | Performs static code analysis |
| Quality Gate | Checks SonarQube quality status |
| Install Dependencies | Installs Node.js dependencies |
| Trivy FS Scan | Scans project files for vulnerabilities |
| Docker Build | Creates the application Docker image |
| Docker Push | Pushes the image to Docker Hub |
| Trivy Image Scan | Scans the Docker image |
| Docker Deployment | Runs the application container |
| Kubernetes Deployment | Deploys the application to AWS EKS |

## Monitoring Setup

### Prometheus

Prometheus is configured to collect metrics from the monitoring environment.

Prometheus configuration includes:
- Prometheus server metrics.
- Node Exporter metrics.
- Jenkins metrics through the Jenkins Prometheus plugin.

Default port: `9090`

### Node Exporter

Node Exporter collects system-level metrics from the EC2 instance.

Default port: `9100`

### Grafana

Grafana is integrated with Prometheus as a data source.

It provides dashboards to visualize infrastructure and Jenkins metrics.

Default port: `3000`

## Important Ports

| Service | Port |
|---|---|
| Jenkins | 8080 |
| SonarQube | 9000 |
| Prometheus | 9090 |
| Node Exporter | 9100 |
| Grafana | 3000 |
| Netflix Application (Docker) | 8081 |
| Netflix Application (Docker) | 3001 |

## Project Execution Steps

1. Launch an Ubuntu 24.04 EC2 instance.
2. Attach the required IAM role.
3. Install Terraform, AWS CLI and kubectl.
4. Install Jenkins, Java, Docker and Trivy.
5. Deploy SonarQube using Docker.
6. Generate a TMDB API key for movie data.
7. Launch a separate monitoring EC2 instance.
8. Install Prometheus, Node Exporter and Grafana.
9. Integrate Prometheus with Jenkins.
10. Configure Jenkins email notifications.
11. Install and configure Jenkins tools and plugins.
12. Configure SonarQube server and authentication.
13. Create the Jenkins CI/CD pipeline.
14. Perform code quality and Trivy filesystem scanning.
15. Build and push the Docker image to Docker Hub.
16. Scan the Docker image using Trivy.
17. Deploy the application using Docker.
18. Provision AWS EKS using Terraform.
19. Configure Jenkins with Kubernetes credentials.
20. Deploy the application using Kubernetes manifests.
21. Access the Netflix Clone application through the browser.
22. Monitor infrastructure and Jenkins metrics using Prometheus and Grafana.
23. Destroy AWS resources after completing the project.

## Learning Outcomes

Through this project, I gained hands-on experience with:

- Building CI/CD pipelines using Jenkins.
- Integrating GitHub with Jenkins.
- Performing static code analysis using SonarQube.
- Implementing vulnerability scanning using Trivy.
- Working with Docker images and containers.
- Automating AWS infrastructure using Terraform.
- Provisioning and managing AWS EKS.
- Deploying applications using Kubernetes.
- Integrating Prometheus and Grafana.
- Monitoring Jenkins and infrastructure metrics.
- Configuring automated email notifications.

## Cleanup

To avoid unnecessary AWS charges:

1. Destroy the EKS infrastructure using Terraform.
2. Remove Kubernetes resources.
3. Stop and terminate EC2 instances when they are no longer required.
4. Remove unused Docker images and containers.
5. Delete unused AWS resources such as load balancers and storage.

## Conclusion

This project demonstrates an end-to-end DevSecOps implementation by integrating CI/CD automation, code quality analysis, security scanning, Docker containerization, Kubernetes orchestration, Infrastructure as Code and monitoring.

It provides practical experience in automating application deployment and managing cloud-native infrastructure using AWS and DevOps tools.

**Project Focus:** CI/CD Automation | DevSecOps | AWS | Docker | Kubernetes | Terraform | Monitoring
