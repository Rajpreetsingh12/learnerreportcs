Learner Report CS: - 

Project Overview: - 

This project is a MERN stack application consisting of a backend, frontend, Helm charts for Kubernetes deployment, and Jenkins configuration for CI/CD. The project structure is as follows. 

learnerReportCS_backend: Contains the backend code (Node.js/Express.js). 

learnerReportCS_frontend: Contains the frontend code (React.js). 

learnerReportDeployment: Contains Kubernetes deployment files. 

learnerReportHelm: Contains Helm charts for deployment. 

learnReport.jenkins: Jenkins pipeline configuration for CI/CD. 

Directory Structure: - 

learnerReportCS/ 

├── learnerReportCS_backend        # Backend code repository 

├── learnerReportCS_frontend       # Frontend code repository 

├── learnerReportDeployment        # Kubernetes deployment files 

├── learnerReportHelm              # Helm charts for Kubernetes 

└── learnReport.jenkins            # Jenkins pipeline configuration 

Setup Instructions:  

1. Clone the Repositories: - 

Clone the main repository which includes submodules for frontend and backend: 
git clone --recurse-submodules https://github.com/Rajpreetsingh12/learnerreportcs.git 

 

2.Backend Setup: - 

Navigate to the learnerReportCS_backend directory. Fill the enviorment variables in config.env and follow these steps: 

cd learnerReportCS_backend 

 

vim config.env # update the env values here 

npm install 

node index.js 
 

 

 

 

 

3. Frontend Setup 

 

 

 

 cd learnerReportCS_frontend 

npm install 

npm start 

 

 

4. Docker Build and Push 
Build and Push Backend Docker Image 

1.Navigate to Backend Directory: 
 

 

2.Build the Docker Image: 

docker build -t learnerreportcsbackend:latest . 

 

 

5.Navigate to Frontend Directory: 
 

 6. Build the Docker Image: 

 

 

7. Kubernetes Deployment 

The learnerReportDeployment directory contains Kubernetes manifests for deploying the application. 

To deploy the application,use the following command: 

 
Update the docker image in deployment files. 

I was getting this below error in the backend_secret.yaml file because there was some syntax and format errors in the same so i changed it to below format:- 

 

 

 

Then my secret_backend.yaml file got created. 
 

 

 

 

 

6. Helm Charts 

Got the errors related to the chart and values.yaml files path so modified the files 

Location in the below strucure and ensured that the helm chart is installed in the  

Project directory. By hitting the command “helm create lernerreporthelm/” 

 

Corrected the directory structure of the files in the templates.yaml and in the 

Lernerreporthelm directory in the below structure 
 

C:/Learnerreportcs/lernerreporthelm/ 

 ├── Chart.yaml ├── values.yaml  

└── templates/ ├── deployment.yaml └── service.yaml 

 

After editing the files according to above strucure  

 

 
 

 

 

Then hit this command helm upgrade --install learnerreport "C:/Learnerreportcs/lernerreporthelm" \ 

  --set backend.image=rajedocker1234/learnerreportcs-backend:backend-${VERSION} \ 

  --set frontend.image=rajedocker1234/learnerreportcs-frontend:frontend-${VERSION} 

 

 

 

7.Jenkins Pipeline 

The learnReport.jenkins file contains the Jenkins pipeline configuration for building and deploying the application. 

  

Ensure Jenkins is configured to use this pipeline script for automated CI/CD. The script builds Docker images, pushes them to Docker Hub, and deploys the application to Kubernetes using Helm. 

 

8. Configure Docker Hub Credentials in Jenkins 

To ensure Docker Hub credentials are correctly configured in Jenkins, follow these steps: 

1. Obtain Docker Hub Credentials: 

Log in to Docker Hub and obtain your Docker Hub username and password. For enhanced security, consider creating and using an access token instead of your password. 

 

 

2. Log in to Jenkins: 

Open your Jenkins instance in a web browser and log in. 

 

From the Jenkins dashboard, click on Manage Jenkins. 

 

 

 

 

 

Select Manage Credentials (or Credentials if you’re using Jenkins with a newer interface). 

 

Select the Appropriate Domain  

 You can add credentials to the global domain or a specific domain. To add them globally, click on (global):- 

 

Add New Credentials: 

Click on Add Credentials. 

 

 

3.Configure Docker Hub Credentials: 

-  kind:Select Username with password. 

   - Scope: Choose Global (or System depending on your requirements). 

    

- Username: Enter your Docker Hub username. 

    

- Password: Enter your Docker Hub password or access token. 

    

- ID: Provide a unique ID for these credentials (e.g., dockerhub-credentials). 

 

Create a New Pipeline Job:  

On the Jenkins dashboard, click on “New Item”. 
 

Select “Pipeline” and click OK. 

 

 

 

Configure the Pipeline: 

Under the General section, you can optionally add a description for the pipeline job 

 

Step 2: Connect to GitHub Repository 

Scroll to the Pipeline Section: 

In the Pipeline section, set Definition to Pipeline script from SCM (Source Control Management). 

 

 

 

 

Set SCM to Git: 

in the SCM dropdown, select Git. 

 

Add GitHub Repository URL: 

In the Repository URL, add the GitHub repository URL where your Jenkinsfile is stored. 

 

 

Add Credentials: 

As my github repository is public so there is no need of adding its creds same as we did 

In case of docker.we need to add the creds in the jenkins if the repository is private. 

 

Select the Branch: 

Under Branches to build, specify the branch where your Jenkinsfile is located, e.g., main or develop. 

 

 

 

 

 

 

Define the Jenkinsfile Structure in Your GitHub Repo 

Insure you have your jenkins pipeline script in the above mentioned github repo. 

 

Save and Build the Pipeline 

 

 
