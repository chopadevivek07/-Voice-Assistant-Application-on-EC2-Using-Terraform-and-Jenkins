# Jarvis Desktop Voice Assistant Deployment on AWS EC2

This project demonstrates how to deploy the **Jarvis Desktop Voice Assistant** on an AWS EC2 instance using **Terraform** for infrastructure provisioning and **Jenkins** for CI/CD automation.

---

## Architecture Diagram
![](/Gemini_Generated_Image_snishysnishysnis.png)

## **Project Overview**

- **Objective:** Automate deployment of the Jarvis Desktop Voice Assistant on AWS EC2 using Terraform and Jenkins.
- **Technologies Used:**
  - **AWS:** EC2 instance
  - **Terraform:** Infrastructure as Code (IaC)
  - **Jenkins:** CI/CD pipeline
  - **GitHub:** Source repository
  - **Python:** Application dependencies
  - **systemd:** Service management on EC2

---

## **Project Workflow**

1. **Terraform Infrastructure Setup**
   - Create EC2 instance.
   - Create security group with SSH access.
   - Create/use SSH key pair.
   - Add user-data to install Python and dependencies.
   - Set up systemd service to run Jarvis automatically.

2. **Jenkins CI/CD Pipeline**
   - Configure GitHub webhook to trigger Jenkins on repository updates.
   - Pipeline stages:
     1. **Prepare:** Validate EC2_HOST parameter.
     2. **Update code on EC2:** Clone or pull the latest repository.
     3. **Install dependencies:** Create Python virtual environment and install requirements.
     4. **Restart service:** Restart the systemd `jarvis.service`.
     5. **Verify:** Show recent logs to confirm the application is running.

---

## **Prerequisites**

- AWS account with EC2 access.
- Terraform installed locally or on Jenkins server.
- Jenkins installed with required plugins:
  - **Pipeline**
  - **SSH Agent**
- SSH private key added in Jenkins credentials (ID: `jarvis-server`).
- Public GitHub repository forked and updated (optional visible change for testing).

---

## **Setup Instructions**

### **1. Terraform Deployment**

```bash
terraform init
terraform plan
terraform apply -auto-approve
```

![](/Images/Screenshot%20(960).png)
                        
### Jenkins Pipeline Setup

1. Create a new **Pipeline** job.

2. Configure **Git SCM** with your repository URL:


3. Add **Build Parameter**:

- Name: `EC2_HOST`  
- Default Value: `<your EC2 public IP>`

4. Add **SSH credentials**:

- ID: `jarvis-server`  
- Username: `ubuntu`  
- Private key: Your `.pem` file

5. Use the provided `Jenkinsfile` in your repository.

6. Run the pipeline.

---

### Pipeline Stages

| Stage                  | Description                                           |
|------------------------|-------------------------------------------------------|
| **Prepare**            | Validate EC2_HOST parameter.                          |
| **Update code on EC2** | Pull latest code or clone repository.                |
| **Install dependencies** | Setup Python virtual environment and install packages. |
| **Restart service**    | Restart Jarvis systemd service.                       |
| **Verify**             | Check application logs for successful deployment.    |

---

### Verify Deployment

- SSH into EC2:

```bash
ssh -i your-key.pem ubuntu@<EC2_HOST>
sudo systemctl status jarvis.service
cd ~/jarvis
```
![](/Images/Screenshot%20(963).png)
![](/Images/Screenshot%20(964).png)

# Conclusion

This project demonstrates a complete DevOps workflow:

Infrastructure as Code using Terraform

CI/CD automation using Jenkins

Automated deployment and service management on AWS EC2

Integrates GitHub updates into a live application deployment

Repository

Forked GitHub repository:
https://github.com/chopadevivek07/Voice-Assistant-Application-on-EC2-Using-Terraform-and-Jenkins

## Author

Vivek Ambadas Chopde

MCA Student | DevOps & Cloud Enthusiast
