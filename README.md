Sum Website

A simple Flask web application that adds two numbers entered by the user.

---

Project Overview

This project is built using Python and Flask. Users enter two numbers in a web form, and the application calculates and displays their sum.

---

Prerequisites

Before running this project, make sure we have:

- Python 3 installed
- Git installed
- A GitHub account
- AWS EC2 instance (for deployment)

Check installation:

python3 --version
git --version


Clone the Repository

Clone the project from GitHub:

git clone https://github.com/YOUR_USERNAME/sum-website.git


Move into the project folder:

cd sum-website

---

Create a Virtual Environment

Create a Python virtual environment:

python3 -m venv venv

Activate it:

source venv/bin/activate

You should see:

(venv)

at the beginning of the terminal line.


---


Install Dependencies

Install required packages:

pip install -r requirements.txt

---

Run the Application Locally

Start the Flask application:

python3 app.py

output:

Running on http://127.0.0.1:5000

Open:

http://localhost:5000

in your browser.

---


Deploy on AWS EC2

Step 1: Launch EC2 Instance

1. Open AWS Console.
2. Launch an Ubuntu EC2 instance.
3. Create or select a key pair.
4. Allow SSH (Port 22).

---

Step 2: Connect to EC2

ssh -i your-key.pem ubuntu@YOUR_PUBLIC_IP

---

Step 3: Install Required Software

sudo apt update
sudo apt install python3 python3-pip git -y

---

Step 4: Clone Project on EC2

git clone https://github.com/YOUR_USERNAME/sum-website.git
cd sum-website

---

Step 5: Create Virtual Environment

python3 -m venv venv
source venv/bin/activate

---

Step 6: Install Dependencies

pip install -r requirements.txt

---

Step 7: Run the Application

python3 app.py

If needed, update app.py:

app.run(host="0.0.0.0", port=5000)

---

Step 8: Open Port 5000

In AWS Security Group:

Add inbound rule:

Type| Port| Source
Custom TCP| 5000| 0.0.0.0/0

---

Step 9: Access Website

Open:

http://YOUR_PUBLIC_IP:5000

---



Run as a Service

Create:

sudo nano /etc/systemd/system/flaskapp.service

Paste:

[Unit]
Description=Flask App
After=network.target

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/sum-website
Environment="PATH=/home/ubuntu/sum-website/venv/bin"
ExecStart=/home/ubuntu/sum-website/venv/bin/python app.py
Restart=always

[Install]
WantedBy=multi-user.target

Enable service:

sudo systemctl daemon-reload
sudo systemctl enable flaskapp
sudo systemctl start flaskapp

Check status:

sudo systemctl status flaskapp

---

Updating the Application

After making changes:

git add .
git commit -m "Update application"
git push origin main

On EC2:

cd sum-website
git pull origin main
sudo systemctl restart flaskapp

---

Future Improvements

- GitHub Actions CI/CD Pipeline
- Docker Support
- HTTPS using SSL
- Custom Domain Name

here i explain in steps for set-up .
