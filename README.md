# Ruby on Rails + AWS Fargate & RDS (via deploy-stack) ☁️🚀

> A production-grade example of a modern Ruby on Rails application deployed to AWS ECS Fargate with a managed PostgreSQL database, generated instantly using the [rails-template-deploy-stack](https://github.com/anton-codes-iac/rails-template-deploy-stack).

[![Ruby on Rails](https://img.shields.io/badge/Ruby_on_Rails-CC0000?style=flat&logo=ruby-on-rails&logoColor=white)](https://rubyonrails.org/)
[![deploy-stack](https://img.shields.io/badge/deploy--stack-CLI-000000?style=flat&logo=amazon-aws&logoColor=white)](https://github.com/anton-codes-iac/deploy-stack)

## 🌟 The Magic

This repository does **not** rely on manual Terraform scripting, AWS console clicks, or wrestling with CI/CD YAML files. 

The AWS architecture, Docker configurations, and GitHub Actions CI/CD pipelines were automatically provisioned the moment the project was scaffolded using a standard Rails application template. 

The template safely backs up the default Rails 8 Dockerfile and replaces it with a highly optimized Alpine multi-stage build. This guarantees **0 CVEs** on security scans, injects the necessary PostgreSQL C-bindings for AWS RDS, and seamlessly executes `deploy-stack` to generate the `terraform/` and `.github/` directories natively.

## 🏗️ Architecture Features

* **Serverless Compute:** AWS ECS Fargate container running a multi-threaded Puma web server behind an unprivileged user.
* **Managed Database:** Securely attached Amazon RDS PostgreSQL instance running inside a private subnet.
* **Traffic Routing:** Application Load Balancer (ALB) handling health checks and traffic distribution.
* **Zero-Secret CI/CD:** GitHub Actions configured with AWS IAM OIDC (no long-lived access keys).
* **DevSecOps Built-in:** Automated container and infrastructure vulnerability scanning via Trivy on every push.

## 🚀 Try It Yourself

Want to bootstrap and deploy your own production-ready Rails app to AWS in under 5 minutes?

1. Scaffold a new Rails application using the remote template:
   ```bash
   rails new my-rails-app -m https://raw.githubusercontent.com/anton-codes-iac/rails-template-deploy-stack/main/template.rb
   ```
2. Navigate into your new project folder:
   ```bash
   cd my-rails-app
   ```
3. Run the deployment command to provision the real infrastructure in your AWS account:
   ```bash
   npx --yes deploy-stack apply
   ```
4. If you enabled a database, push your local API secrets (like `RAILS_MASTER_KEY` or database passwords) to the newly created AWS Vault:
   ```bash
   npx --yes deploy-stack secrets push .env
   ```

## 🛑 Safe Teardown

To destroy the AWS infrastructure provisioned by this example (including the RDS database) and stop all billing, run:
```bash
npx --yes deploy-stack destroy
```

## 💰 AWS Costs & Disclaimer
**This tool provisions real AWS resources which will incur charges on your AWS bill.** An ECS Fargate cluster with an Application Load Balancer running 24/7 typically costs around ~$15 - $20/month minimum, depending on your region. A managed RDS database will add additional monthly costs.

*Disclaimer: The maintainers are not responsible for unexpected AWS charges. Always monitor your AWS Billing Dashboard.*