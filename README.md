# Akaunting AWS Infrastructure

This repository contains AWS CloudFormation templates for deploying Akaunting, a free and open-source accounting software, on AWS Free Tier compatible resources.

## Overview

Akaunting is a modern accounting software designed for small businesses and freelancers. This project provides automated infrastructure deployment using AWS CloudFormation, ensuring:

- Cost-effective deployment within AWS Free Tier limits
- Secure infrastructure configuration
- Automated installation and configuration
- Production-ready deployment

## Architecture

![Akaunting AWS Architecture](https://raw.githubusercontent.com/sergiocoding96/akaunting-aws-infrastructure/main/architecture.png)

The infrastructure includes:
- VPC with public and private subnets
- EC2 t2.micro instance (Free Tier eligible)
- MariaDB database on the EC2 instance
- Security groups for appropriate network access
- IAM roles with minimal required permissions
- Elastic IP for stable access

## Quick Start

### Option 1: Combined Template (Recommended)

1. Go to AWS CloudFormation console
2. Click "Create stack" > "With new resources (standard)"
3. Choose "Upload a template file"
4. Upload `akaunting-combined.yaml`
5. Enter stack details:
   - Stack name: `akaunting-stack`
   - DBPassword: Create a secure password (e.g., `Akaunting2024!`)
   - EnvironmentType: Choose from development, staging, or production
   - KeyName: Select an existing EC2 key pair for SSH access
6. Click through the next screens, acknowledge IAM capabilities
7. Click "Create stack"

### Option 2: Individual Templates

For more customized deployments, you can use the individual templates:
1. Deploy `vpc.yaml` first
2. Deploy `ec2.yaml` using the outputs from the VPC stack
3. (Optional) Deploy `rds.yaml` if you prefer an external database

## Implementation Details

### Security Considerations

- EC2 instance is configured with security groups allowing only necessary traffic
- HTTPS can be enabled by adding a certificate (see Next Steps)
- All passwords and credentials can be customized during deployment

### Maintenance

- OS updates are automatically applied during installation
- Database backups should be configured separately (see Next Steps)
- For production use, consider adding additional security measures

## Free Tier Usage

All resources are configured to stay within AWS Free Tier limits:
- EC2: t2.micro (750 hours/month free)
- Storage: Under 30GB total
- Data Transfer: Within free tier limits

## Next Steps

1. **Enable HTTPS**: Use AWS Certificate Manager and configure SSL/TLS
2. **Implement Backups**: Set up automated database backups
3. **Monitoring**: Add CloudWatch alarms for resource monitoring
4. **High Availability**: Implement multi-AZ deployment for production
5. **CI/CD Pipeline**: Set up automated deployment pipeline

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.