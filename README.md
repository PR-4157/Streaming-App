# StreamingApp DevOps Project (Orchestration & Scaling)

Stream premium video content, host live watch parties, and manage your catalogue with a modern microservice architecture. The platform now ships with a production-ready admin portal, real-time chat, S3-backed adaptive streaming, and a redesigned cinematic frontend experience.

## Overview 
- This project demonstrates end-to-end DevOps implementation for a MERN stack application using:

* Containerization with Docker
* CI/CD using Jenkins
* Deployment on AWS EKS (Kubernetes)
* Monitoring with CloudWatch
* (Bonus) ChatOps integration

## Architecture
GitHub → Jenkins → Docker → AWS ECR → AWS EKS → CloudWatch
- Flow:

1. Code pushed to GitHub
2. Jenkins triggers pipeline
3. Docker images built & pushed to ECR
4. Kubernetes (EKS) deploys app using Helm
5. Monitoring via CloudWatch

## Project Structure 
StreamingApp/
│
├── frontend/
│   ├── Dockerfile
│   └── source code
│
├── backend/
│   ├── Dockerfile
│   └── source code
│
├── helm/
│   └── charts for deployment
│
├── Jenkinsfile
└── README.md

## Step 1: Version Control
git clone https://github.com/PR-4157/Streaming_App.git
cd Streaming_App
<img width="663" height="357" alt="Screenshot 2026-05-02 at 7 37 36 PM" src="https://github.com/user-attachments/assets/5ef637c1-a0fd-4e13-ba59-d2892bba7449" />

git remote add upstream https://github.com/UnpredictablePrashant/StreamingApp.git
git pull upstream main
<img width="664" height="236" alt="Screenshot 2026-05-02 at 7 40 25 PM" src="https://github.com/user-attachments/assets/012f0a8d-6374-4cee-b11f-a16f10dfd8e6" />

## Step 2: Dockerization
<img width="660" height="381" alt="Screenshot 2026-05-02 at 7 40 36 PM" src="https://github.com/user-attachments/assets/5f63b210-ffb4-4e20-b593-c8837ba07d62" />
<img width="661" height="227" alt="Screenshot 2026-05-02 at 7 41 43 PM" src="https://github.com/user-attachments/assets/dfbe643b-6b67-42ed-a9b4-39558a7290d1" />
<img width="658" height="106" alt="Screenshot 2026-05-02 at 7 42 36 PM" src="https://github.com/user-attachments/assets/1f2f78cb-0a85-4f52-9180-f18ad9ceb76c" />
<img width="663" height="269" alt="Screenshot 2026-05-02 at 7 42 19 PM" src="https://github.com/user-attachments/assets/bdb22675-5286-4bbc-848b-bb1754b9ecf6" />

docker build -t frontend ./frontend
<img width="661" height="377" alt="Screenshot 2026-05-02 at 8 40 09 PM" src="https://github.com/user-attachments/assets/67cd0a9a-25c8-4024-9b6c-ab93d8546f59" />
docker build -t backend ./backend
<img width="657" height="489" alt="Screenshot 2026-05-02 at 9 48 04 PM" src="https://github.com/user-attachments/assets/d046719d-a902-4897-822e-bd81bb5a2690" />

## Step 3: Push to AWS ECR
1.Created ECR repos
2.Login Docker to AWS
3. Pushed images 
So first I have created IAM user and assigned security credential to login via Aws CLI 

<img width="1140" height="632" alt="Screenshot 2026-05-02 at 8 08 11 PM" src="https://github.com/user-attachments/assets/6a862dd8-80b5-4e3d-907a-3e9762d0d196" />
aws ecr get-login-password --region ap-south-1 \
| docker login --username AWS --password-stdin <account-id>.dkr.ecr.ap-south-1.amazonaws.com
<img width="665" height="164" alt="Screenshot 2026-05-02 at 8 39 46 PM" src="https://github.com/user-attachments/assets/e4894808-2bc1-4c3a-a3a7-66ca8c5bd24e" />

docker tag frontend:latest <ECR-URI>/frontend
docker push <ECR-URI>/frontend
<img width="663" height="293" alt="Screenshot 2026-05-02 at 9 01 23 PM" src="https://github.com/user-attachments/assets/f73019d5-8e59-43ef-8660-ddc7fb69a70e" />

docker tag backend:latest <ECR-URI>/backend
docker push <ECR-URI>/backend
<img width="660" height="253" alt="Screenshot 2026-05-02 at 9 54 22 PM" src="https://github.com/user-attachments/assets/25ef2a53-c39d-48f1-8586-c1a8a9dc1765" />

## Till now we have completed  
✔ Backend Docker ✅ 
✔ MongoDB connection ✅ 
✔ Docker networking ✅ 
✔ Frontend Docker ✅ 
✔ Full MERN app running locally ✅ 

## EXPECTED OUTPUT 
<img width="837" height="498" alt="Screenshot 2026-05-02 at 10 19 32 PM" src="https://github.com/user-attachments/assets/bd806459-f66c-4091-a660-c089b8c29bc1" />
After Process:
<img width="838" height="493" alt="Screenshot 2026-05-02 at 10 19 46 PM" src="https://github.com/user-attachments/assets/6d1d7515-8e62-4e68-a032-3a3cc6ad494e" />

## Verifying in AWS CONSOLE 
Checking ECR → Repositories 
Click: 
* backend
* frontend
<img width="1140" height="632" alt="Screenshot 2026-05-02 at 8 08 11 PM" src="https://github.com/user-attachments/assets/1ab15b5d-55af-40f0-83af-9904e9368387" />
<img width="1512" height="982" alt="Screenshot 2026-05-02 at 10 24 01 PM" src="https://github.com/user-attachments/assets/20617022-ae0d-4de0-8d8f-a4f07219c350" />
<img width="1512" height="982" alt="Screenshot 2026-05-02 at 10 24 24 PM" src="https://github.com/user-attachments/assets/934d8d27-c116-4701-913f-618a251954c1" />

## Summary 
This project successfully demonstrates how to build a production-ready DevOps pipeline using industry-standard tools. It integrates version control, containerization, CI/CD automation, and Kubernetes orchestration into a unified workflow.
By leveraging AWS services like ECR, EKS, and CloudWatch, the application achieves scalability, reliability, and observability, making it suitable for real-world deployment scenarios.

## Conclusion
The implementation highlights the importance of automation and orchestration in modern software delivery. Using tools like Jenkins, Docker, and Kubernetes, the deployment process becomes faster, consistent, and scalable.
This project provides a strong foundation for understanding cloud-native DevOps practices and can be extended further with advanced strategies like Infrastructure as Code, automated scaling, and multi-environment deployments.
