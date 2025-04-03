### **ec2-setup.md (AWS EC2 & Docker Setup)**  

#### **1. Launch EC2 Instance**  
- Go to **AWS Console → EC2 → Launch Instance**.  
- Select **Amazon Linux 2** (t2.micro - Free Tier).  
- Enable **SSH (port 22) & HTTP (port 80)** in Security Groups.  

#### **2. Install Docker**  
```sh
sudo yum install -y docker  
sudo service docker start  
sudo usermod -aG docker ec2-user  
```
(Reboot or log out and back in for changes to apply.)  

#### **3. Run the Node.js App**  
```sh
docker run --rm -p 80:3000 \
-e DB_HOST="your-db-endpoint" \
-e DB_USER="admin" \
-e DB_PASSWORD="your-password" \
-d philippaul/node-mysql-app:02
```

#### **4. Access the Application**  
- Open **http://<your-ec2-public-ip>** in a browser.
