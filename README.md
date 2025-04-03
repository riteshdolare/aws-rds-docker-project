# **AWS RDS + Docker Deployment**  

## **Overview**  
This project demonstrates how to deploy a **containerized Node.js application** using **AWS RDS (MySQL) and Docker on an EC2 instance**. The application runs inside a **Docker container**, while the database is hosted on **AWS RDS** for better scalability and management.  

## **Technologies Used**  
- **AWS RDS** – Managed MySQL database service  
- **AWS EC2** – Virtual server for hosting the application  
- **Docker** – Containerization platform for application deployment  
- **Node.js** – Backend runtime environment  
- **MySQL** – Relational database system  

## **Prerequisites**  
Before proceeding with the deployment, ensure you have:  
- An **AWS account**  
- **AWS CLI** installed and configured  
- SSH access to an **AWS EC2 instance**  

---

## **Deployment Steps**  

### **1. Set Up AWS RDS (MySQL)**  
Follow the instructions in [`rds-setup.md`](rds-setup.md) to:  
- Create an **AWS RDS MySQL** instance  
- Configure **security groups** to allow database access  

### **2. Launch an EC2 Instance & Install Docker**  
Refer to [`ec2-setup.md`](ec2-setup.md) for step-by-step guidance on:  
- Creating an **EC2 instance**  
- Installing **Docker** on the server  

### **3. Deploy the Node.js Application**  
Run the following command on your **EC2 instance** to pull and run the prebuilt Docker image:  
```sh
docker run --rm -p 80:3000 \
-e DB_HOST="your-db-hostname" \
-e DB_USER="your-db-username" \
-e DB_PASSWORD="your-db-password" \
-d philippaul/node-mysql-app:02
```
Replace:  
- `"your-db-hostname"` with your **AWS RDS endpoint**  
- `"your-db-username"` with your **MySQL username**  
- `"your-db-password"` with your **MySQL password**  

### **4. Connect to the MySQL Database from EC2**  
To test the MySQL connection, run the following command from the EC2 instance:  
```sh
docker run -it --rm mysql:8.0 mysql -h your-db-hostname -u admin -p
```
Enter the **database password** when prompted.  

### **5. Access the Application**  
Once the container is running, open a browser and navigate to:  
```sh
http://<your-ec2-public-ip>
```
You should see the deployed application.  

---

## **Security Considerations**  
- Ensure **your RDS instance is not publicly accessible** unless necessary.  
- Use **IAM roles** and **security groups** to limit access to the database.  
- Do not hardcode database credentials—use **environment variables** or AWS Secrets Manager.  

---

## **Troubleshooting**  

### **1. Check Running Containers**  
```sh
docker ps
```
If the container is not running, check logs:  
```sh
docker logs <container_id>
```

### **2. Verify EC2 Security Group Rules**  
Ensure the **EC2 security group** allows:  
- **Inbound traffic on port 80** (for HTTP access)  
- **Outbound access to MySQL (port 3306)**  

### **3. Verify RDS Security Group Rules**  
Ensure **RDS security group** allows:  
- **Inbound connections from EC2 on port 3306**  

### **4. Test MySQL Connectivity from EC2**  
Run:  
```sh
telnet your-db-hostname 3306
```
If the connection fails, update **security groups** to allow EC2 to access RDS.  

---

## **Conclusion**  
By following these steps, you can successfully deploy a **Node.js application** using **AWS RDS and Docker** on **AWS EC2**. This setup ensures **scalability, flexibility, and ease of deployment**.  
