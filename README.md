Lab 1 – Terraform Infrastructure on Google Cloud
Project Overview

This project demonstrates Infrastructure as Code using Terraform to deploy a secure virtual machine in Google Cloud Platform (GCP).
The Terraform configuration creates a Compute Engine VM running Ubuntu 22.04 and includes a daily disk snapshot backup policy to protect data.

The repository also includes a GitHub Actions CI pipeline that automatically checks Terraform formatting, runs a security scan, and validates the configuration whenever changes are pushed or a pull request is created.

This project demonstrates basic DevSecOps practices, combining infrastructure automation, CI validation, and system hardening.

How to Run the Project
1. Clone the repository
git clone https://github.com/viktorwesterlund-cmd/lab1-terraform.git
cd lab1-terraform
2. Initialize Terraform
terraform init
3. Validate configuration
terraform validate
4. Review execution plan
terraform plan
5. Apply infrastructure
terraform apply

Confirm with:

yes

Terraform will create the VM and configure the backup snapshot policy in the GCP project.

CI Pipeline

The project uses GitHub Actions to automatically validate Terraform code.

The pipeline performs the following checks:

Terraform formatting check (terraform fmt)

Security scanning with Trivy

Terraform configuration validation

<img width="1352" height="588" alt="pull request" src="https://github.com/user-attachments/assets/93de078c-e861-4ccc-b3f3-4a9feeb90d8b" />


GCP VM Deployment

After running terraform apply, the virtual machine is created in Google Cloud.

You can view it in:

GCP Console → Compute Engine → VM Instances

VM Screenshot

Insert screenshot of the created VM instance from the GCP Console.

Security Decisions

The VM uses a startup script to apply basic security hardening during creation.

UFW (Uncomplicated Firewall)

UFW is enabled to control incoming and outgoing network traffic.

Configuration:

Default deny incoming connections

Allow outgoing traffic

Allow SSH access

This reduces the attack surface and prevents unauthorized access.

Fail2Ban

Fail2Ban monitors log files for suspicious login attempts and automatically blocks IP addresses that repeatedly fail authentication.

Benefits:

Prevents brute-force attacks

Automatically blocks malicious IP addresses

Unattended Upgrades

Automatic security updates are enabled using unattended-upgrades.

Benefits:

Automatically installs security patches

Reduces risk of vulnerabilities from outdated packages

Backup Strategy

A daily snapshot policy is configured using Terraform.

Features:

Daily snapshots

Retention period of 7 days

Snapshots preserved even if the original disk is deleted

This ensures recoverability in case of system failure or accidental data loss.

Repository

GitHub repository:

https://github.com/viktorwesterlund-cmd/lab1-terraform

Author

DevSecOps – Lab 1
CHAS Academy
