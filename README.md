🚀 Cloud Troubleshooting Lab (AWS Project)
📌 Project Overview

This project demonstrates real-world cloud troubleshooting scenarios using AWS services.
Instead of just deploying infrastructure, I intentionally simulated failures and resolved them using a structured troubleshooting approach.

🎯 Objective

1.Understand how real production issues occur
2.Practice troubleshooting in AWS
3.Learn monitoring using CloudWatch
4.Implement alerting using SNS
5.Think like a Cloud Support Engineer

🏗️ Architecture
Components Used:

-AWS EC2 (Web Server)

-Apache (httpd)

-AWS CloudWatch (Monitoring)

-AWS SNS (Alerting)

-Security Groups (Firewall)

⚙️ Setup Steps
1. Launch EC2 Instance
![EC2 Running](screenshots/1-ec2-running.png)

AMI: Amazon Linux 2

Instance Type: t2.micro

Enabled:

SSH (22)
HTTP (80)

2. Connect to Instance
ssh -i lab-key.pem ec2-user@<public-ip>

3. Install Apache
sudo yum update -y
sudo yum install httpd -y

4. Start Web Server
sudo systemctl start httpd
sudo systemctl enable httpd

5. Create Website
echo "Hello Cloud/DevOps World" | sudo tee /var/www/html/index.html
✅ Result

Website successfully hosted on EC2.

🧪 Troubleshooting Scenarios

🔴 Scenario 1: Website Down (Security Group Issue)

Problem:
Website not accessible in browser

Cause:

Port 80 removed from Security Group

#Troubleshooting:

Checked EC2 status → Running

Checked network rules → HTTP missing

Fix:
Added HTTP (port 80) rule

Learning:
Network rules can block access even if server is running.

🔴 Scenario 2: Apache Service Stopped

Problem:
Website not loading

Cause:
Apache service stopped

Command Used:
sudo systemctl stop httpd
Troubleshooting:

Checked service status

Fix:
sudo systemctl start httpd

Learning:
Infrastructure running ≠ Application running

🔴 Scenario 3: High CPU Usage

Problem:
Server became slow

Cause:
Multiple CPU-intensive processes

Command Used:
yes > /dev/null &

Troubleshooting:
Used top command

Observed CPU = 100%

Identified yes processes

Fix:
killall yes

Learning:
High CPU causes performance degradation

🔴 Scenario 4: SSH Not Working

Problem:
Unable to connect to EC2

Cause:
Port 22 removed from Security Group

Troubleshooting:
Checked security group rules

Fix:
Allowed SSH (port 22)

Learning:
Connectivity depends on open network paths

🔴 Scenario 5: File Permission Issue

Problem:
Website showing error

Cause:
Incorrect file permissions

Command Used:
sudo chmod 000 /var/www/html/index.html

Fix:
sudo chmod 644 /var/www/html/index.html

Learning:
File permissions directly affect application behavior

🔴 Scenario 6: Log-Based Troubleshooting

Command:
sudo tail -f /var/log/httpd/error_log

Learning:
Logs are the primary source for identifying root causes

📊 Monitoring with CloudWatch

-Monitored CPU Utilization

-Observed spikes during stress testing

-Correlated system behavior with metrics

🚨 Alerting Setup (CloudWatch + SNS)

Steps:

-Created SNS Topic

-Subscribed email

-Created CloudWatch Alarm:

-Metric: CPUUtilization

-Threshold: > 70

#Result:
When CPU crossed threshold → alert triggered
Email notification received

🧠 Troubleshooting Approach

I followed a structured approach:
-Identify problem type
-Check system metrics
-Analyze logs
-Verify configuration
-Fix root cause

🔥 Key Learnings

Troubleshooting is more important than deployment

Monitoring helps identify issues faster

Alerts enable proactive response

Logs are critical for debugging

Cloud systems require layered analysis

🎯 Skills Demonstrated

-AWS EC2 management

-Linux troubleshooting

-CloudWatch monitoring

-SNS alerting

-Networking fundamentals

-Performance debugging

🚀 Conclusion

This project helped me understand how real-world cloud issues occur and how to resolve them efficiently using a structured approach.

📸 Screenshots (Add Here)

EC2 running instance

Website working

CPU spike graph

Alarm triggered

Error scenarios

👨‍💻 Author

Devraj Singh Kholiya
