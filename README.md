# CloudFormationVPC

Alpha-Bravo Multi-VPC Infrastructure
Overview
This CloudFormation project provisions a dual-VPC architecture ("Alpha" and "Bravo") interconnected via AWS Transit Gateway. It is built for secure, scalable networking with centralized logging, IAM roles for SSM-based management, endpoint connectivity, and fine-grained network access controls.

Stack Components
1. Master Stack (master-stack.yaml)
Orchestrates all nested stacks.

Passes parameters and manages dependencies between stacks.

2. Networking Stack (networking.yaml)
Creates:

Two VPCs: Alpha and Bravo

Public & private subnets in three AZs each

Internet Gateways and NAT Gateways

Transit Gateway and VPC attachments

Flow logs with CloudWatch integration

DHCP Options Set

3. Security Stack (security.yaml)
Creates:

NACLs for public and private subnets

Subnet-NACL associations

Security Groups for Alpha, Bravo, and shared use

Enforces:

ICMP between VPCs

Inbound HTTP/HTTPS/SSH to public subnets

Ephemeral port and deny rules for private subnets

4. Endpoints Stack (endpoints.yaml)
Configures:

Interface Endpoints for SSM, EC2Messages, SSMMessages

Gateway Endpoints for S3

Dedicated security groups per VPC for endpoint traffic

5. Compute Stack (compute.yaml)
Defines:

IAM role for EC2 SSM management

Instance profile

Grants:

Core SSM permissions + granular access to SSM, EC2Messages, and related APIs

Prerequisites
AWS CLI configured with adequate IAM permissions.

S3 bucket with all nested templates (networking.yaml, security.yaml, etc.) hosted under the path:
https://alpha-bravo-cloudformation-templates.s3.us-east-1.amazonaws.com/alpha-bravo-lab/
