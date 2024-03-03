# CI-CD_Pipeline
The project is based on a comprehensive CI/CD pipeline with a focus on security best practices and DevSecOps principles. <br>
Range of tools were utilized including Git, GitHub, Jenkins, Maven, SonarQube, Docker, Trivy, AWS, Docker Hub, Kubernetes, and HashiCorp Vault to achieve the desired objectives.<br>

## Tools Used
1. __Git:__ Version control system used for managing source code.<br>
2. __GitHub:__ Hosting service for Git repositories, facilitating collaboration and version control.<br>
3. __Jenkins:__ Automation server used for continuous integration and continuous deployment.<br>
4. __Maven:__ Build automation tool primarily used for Java projects.<br>
5. __SonarQube:__ Code quality and security analysis tool.<br>
6. __Docker:__ Containerization platform used for packaging applications and their dependencies.<br>
7. __Trivy:__ Vulnerability scanner for containers, ensuring container security.<br>
8. __AWS (Amazon Web Services):__ Cloud computing platform providing a range of services for building and deploying applications.<br>
9. __Docker Hub:-__ Cloud-based repository for Docker container images.<br>
10. __Kubernetes:__ Container orchestration platform for automating deployment, scaling, and management of containerized applications.<br>

## Objectives
1. Implement a CI/CD pipeline to automate the software delivery process.<br>
2. Ensure security best practices are integrated throughout the pipeline.<br>
3. Foster collaboration and streamline development workflows using version control and automation.<br>
4. Utilize containerization for consistent deployment environments and scalability.<br>
5. Leverage cloud services for infrastructure provisioning and deployment.<br>

## Project Architecture
![WhatsApp Image 2024-02-12 at 1 10 12 AM (1)](https://github.com/Anuja-J/CI-CD_Pipeline/assets/86790119/d4d69b73-0d46-4899-8015-8d4306d24e90)

## Pipeline flow
1. Jenkins will fetch the code from remote repository.<br>
2. Maven will build the code, if the build fails, the whole pipeline will become a failure and Jenkins will notify the user.<br>
3. If build success then SonarQube scanner will scan the code and will send the report to the SonarQube server, where the report will go through the quality gate and gives the output to the web Dashboard. In the quality gate, we define conditions or rules like how many bugs or vulnerabilities, or code smells should be present in the code. If the quality gate status becomes a failure, the whole pipeline will become a failure then Jenkins will notify the user that your build fails.<br>
4. After the quality gate passes, Docker will build the docker image. if the docker build fails then the whole pipeline will become a failure and Jenkins will notify the user that your build fails.<br>
5. Trivy will scan the docker image, if it finds any Vulnerability then the whole pipeline will become a failure, and the generated report will be sent to Jenkins.<br>
6. After the docker push, Jenkins will create deployment and service in minikube and our application will be deployed into Kubernetes. if Jenkins fails to create deployment and service in Kubernetes, the whole pipeline will become a failure and Jenkins will notify the user that your build fails.<br>

## Project Implementation

1. __Set Up Jenkins and Required Plugins:__
Install Jenkins on your server.<br>
Install necessary plugins like Git, Maven, SonarQube Scanner, Docker, Kubernetes, etc.<br>

2. __Configure Jenkins:__
Configure Jenkins credentials to access your Git repository, SonarQube server, Docker registry, and Kubernetes cluster.<br>

3. __Create Jenkins Pipeline Script:__
Write a Jenkins pipeline script (Jenkinsfile) to define your CI/CD pipeline stages.<br>
Pipeline Stages:<br>
a. Checkout Code from Git: Jenkins will fetch the code from the remote repository.<br>
b. Build with Maven: Maven will build the code. If the build fails, the pipeline will fail, and Jenkins will notify the user.<br>
c. Scan with SonarQube: SonarQube scanner will scan the code and send the report to the SonarQube server. Quality gate conditions/rules will be defined in SonarQube. If the quality gate fails, the pipeline will fail, and Jenkins will notify the user.<br>
d. Build Docker Image: Docker will build the Docker image. If the Docker build fails, the pipeline will fail, and Jenkins will notify the user.<br>
e. Scan Docker Image with Trivy: Trivy will scan the Docker image for vulnerabilities. If any vulnerabilities are found, the pipeline will fail, and the report will be sent to Jenkins.<br>
f. Deploy to Kubernetes: Jenkins will create deployment and service in Minikube. If Jenkins fails to create deployment and service in Kubernetes, the pipeline will fail, and Jenkins will notify the user.<br>

Refer for Pipeline Script: https://github.com/Anuja-J/CI-CD_Pipeline/blob/main/script.txt <br>

4. __Test the Pipeline:__
Test the pipeline with sample code changes to ensure all stages work as expected.<br>


5. __Monitor and Maintain:__
Monitor the pipeline regularly for any failures or issues.<br>
Update and maintain the pipeline as needed.<br>

6. __Documentation:__
Document the pipeline setup and configurations for future reference.<br>

By following these steps, you can set up a CI/CD pipeline using Jenkins to automate the process of fetching code, building, testing, and deploying your application while ensuring code quality and security.










