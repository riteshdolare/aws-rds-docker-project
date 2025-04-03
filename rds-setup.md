### **rds-setup.md (AWS RDS MySQL Setup)**  

#### **1. Create RDS MySQL Instance**  
- Go to **AWS Console → RDS → Create database**.  
- Select **MySQL**, choose **Free Tier (db.t3.micro)**.  
- Set:  
  - **Username**: `admin`  
  - **Password**: Choose a password (no special characters).  
- Enable **Public Access**.  

#### **2. Configure Security Group**  
- Allow **Inbound Rule: TCP 3306** from **0.0.0.0/0** (or restrict as needed).  

#### **3. Get Database Endpoint**  
- Go to **RDS → Databases**, copy the **endpoint (hostname)**.  
