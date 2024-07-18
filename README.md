#!/bin/bash

# Variables
REPO_URL="https://github.com/your-username/AWS-demo-pro.git"
WEB_DIR="/var/www/html"

# Clone the repository
cd /home/ubuntu
git clone $REPO_URL
cd AWS-demo-pro

# Switch to root user
sudo su root << EOF

# Install Apache2
apt update
apt install apache2 -y

# Copy files to Apache web directory
cp index.html $WEB_DIR/
cp -r images/ $WEB_DIR/
cp -r error/ $WEB_DIR/

# Start Apache2 service
systemctl start apache2

EOF

# Output public IP address
PUBLIC_IP=$(curl -s http://169.254.169.254/latest/meta-data/public-ipv4)
echo "Access your site at: http://$PUBLIC_IP"
