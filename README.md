Kubernetes Assignment:  
==========
Create Kubernetes Pods for the following applications:
- tomcat
- Jenkins
- mongo

---

Files in Repository

| File Name                                | Description                            |
| ---------------------------------------- | -------------------------------------- |
| `tomcat-pod.yaml`                        | Deploys a Tomcat application pod       |
| `jenkins-pod.yaml`                       | Deploys a Jenkins CI/CD pod            |
| `mongoDB-pod.yaml`                       | Deploys a MongoDB database pod         |

---

Step 1: Git Setup and Push Commands

Use these commands on your local machine (Git Bash) to initialize and push your project to GitHub.

# Check Git version
git --version

# Configure your Git identity
git config --global user.name "YourName"
git config --global user.email "your@email.com"

# Create project directory and navigate to it
mkdir k8s-assignment
cd k8s-assignment

---

# Copy YAML files from EC2 to your local folder

scp -i "path/to/your-key.pem" ubuntu@ip-172-31-42-25:~/*.yaml /d/devops/kkdevopslearning/pem/k8s-assignment/
eg: scp -i "D:/devops/pem/Master.pem" ubuntu@172.31.42.25:~/*.yaml /d/devops/pem/k8s-assignment/

# Initialize Git repo
git init

# Add and commit files
git add .
git commit -m "Added Kubernetes pod YAMLs for Tomcat, Jenkins, and Mongo"

# Connect to GitHub and push
git remote add origin https://github.com/yourusername/k8s-pods-assignment.git
git branch -M main
git push -u origin main

----

Step 2: Connect to EC2 Instance

Your Kubernetes cluster is set up inside your EC2 instance.
Use this command to connect to it:

ssh -i "D:/devops/pem/Master.pem" ubuntu@172.31.42.25

Step 3: Kubernetes Commands

Once inside your EC2 terminal, you can run these commands to check the cluster, pods, and logs:

# View all pods in all namespaces
kubectl get pods -A

# Describe a specific pod
kubectl describe pod tomcat-pod -n app-ns

# Get Pod Details (Node, IP, Namespace)

kubectl get pods -o wide -n app-ns
kubectl get pods -o wide -n db-ns
kubectl get pods -o wide -n prod

# OR show all pods in all namespaces 
kubectl get pods -A -o wide


# Check Tomcat logs
kubectl logs tomcat-pod -n app-ns



Notes

- Run kubectl commands only inside EC2, where Kubernetes is installed.

- Run git commands only on your local system (Windows Git Bash).

- Always use the correct .pem key when connecting to EC2.

- If you see:
`No resources found in default namespace` → your pods are running in other namespaces (like `app-ns`, `db-ns`, etc.).





