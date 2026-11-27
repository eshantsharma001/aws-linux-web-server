# Project 1: AWS Linux Web Server

Hands-on cloud administration project deploying an Ubuntu web server inside a custom AWS VPC (`eshant-project1-vpc`) in `ap-southeast-2`, serving a custom site via Nginx on Port 80, attaching a persistent EBS volume at `/mnt/ebs-data`, backing up to Amazon S3 (`eshant-project1-backups`) using IAM role `eshant-ec2-s3-backup-role`, and checking CloudWatch metrics for `eshant-project1-web` (`i-0183470489777ae26`, public IP `52.65.32.143`).

## Stack & Resources
- **Region:** `ap-southeast-2`
- **VPC & EC2:** `eshant-project1-vpc` / `eshant-project1-web` (`i-0183470489777ae26`, public IP `52.65.32.143`)
- **Web Server:** Nginx serving `/var/www/html/index.html` over Port 80
- **Storage:** `9.8G` `ext4` EBS volume mounted at `/mnt/ebs-data` via `/etc/fstab`
- **Backup & IAM:** `site-backup.tar.gz` uploaded to `s3://eshant-project1-backups/project1/` via `eshant-ec2-s3-backup-role`
- **Monitoring:** Amazon CloudWatch (`CPU utilization (%)` and network metrics)

## Repository Structure
- `README.md` — Project overview, architecture details, commands, and verification screenshot
- `index.html` — Web page served by Nginx on Port 80
- `screenshots/CPU utilization.png` — Amazon CloudWatch CPU utilization screenshot

## Key Commands
bash
sudo nginx -t && sudo systemctl reload nginx
df -h /mnt/ebs-data
aws s3 cp /mnt/ebs-data/backups/site-backup.tar.gz s3://eshant-project1-backups/project1/ --region ap-southeast-2
aws s3 ls s3://eshant-project1-backups/project1/ --region ap-southeast-2
## Setup & Cleanup Notes
- **Security Group:** Inbound rules allowed SSH (Port 22) for administration and HTTP (Port 80) for web traffic.
- **Decommissioning:** AWS resources in `ap-southeast-2` were cleaned up after archiving the project to GitHub, so the public IP (`52.65.32.143`) is no longer active.

## CloudWatch Verification
![CPU Utilization](screenshots/CPU%20utilization.png)
