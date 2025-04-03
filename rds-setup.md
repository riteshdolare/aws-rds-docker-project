# AWS RDS MySQL Setup Guide

## 1. Create an RDS MySQL Instance
- Go to the AWS Console → RDS → "Create database".
- Select "MySQL" as the database engine.
- Choose "Free Tier" (db.t3.micro).
- Set:
  - **Username**: `admin`
  - **Password**: Choose a password (No special characters).
- Enable "Public Access" to allow connections from anywhere.

## 2. Configure Security Group
- Allow inbound connections on **port 3306** from **anywhere (0.0.0.0/0)**.
- Save and launch the database.

## 3. Get Database Endpoint
- Once the instance is available, go to **RDS → Databases**.
- Copy the **endpoint (hostname)**. You'll use this in your EC2 instance.
