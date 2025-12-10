# CloudBurn

[![Install from GitHub Marketplace](https://img.shields.io/badge/Install-GitHub%20Marketplace-blue?logo=github)](https://github.com/marketplace/cloudburn-io)
[![Documentation](https://img.shields.io/badge/Docs-cloudburn.io-brightgreen)](https://cloudburn.io/docs)
[![Roadmap](https://img.shields.io/badge/Roadmap-View-orange)](https://roadmap.cloudburn.io)

**See AWS costs in your pull requests before deploying to production.**

[CloudBurn](https://cloudburn.io) analyzes your Terraform or AWS CDK infrastructure changes and automatically posts cost estimates in pull requests. Catch expensive mistakes during code review instead of discovering them weeks later on your AWS bill.

## What You Get

- **Automatic cost analysis** on every PR with infrastructure changes
- **Real-time AWS pricing** based on your infrastructure's region
- **Resource-by-resource breakdown** showing old vs new monthly costs
- **Smart filtering** - only shows resources with actual cost impact (VPC, IAM, security groups filtered out)

## Example Output

Here's what CloudBurn posts in your PR:

<!-- cloudburn-cost-report -->

### Infrastructure diff cost report

| Resource         | Current cost | New monthly cost        |
| ---------------- | ------------ | ----------------------- |
| MySecondInstance | $0.00        | $133.15 (+$133.15, new) |
| MyThirdInstance  | $0.00        | $66.58 (+$66.58, new)   |
| firstTaskDef     | $0.00        | $9.01 (+$9.01, new)     |
| MyFirstInstance  | $0.00        | $8.32 (+$8.32, new)     |

Overall monthly cost change: +$217.06

<details><summary><b>Cost details</b></summary>

### MyFirstInstance

- **Hourly price:** $0.0114000000 Hrs
- **Usage Type:** EU-BoxUsage:t3.micro
- **Description:** $0.0114 per On Demand Linux t3.micro Instance Hour

### MySecondInstance

- **Hourly price:** $0.1824000000 Hrs
- **Usage Type:** EU-BoxUsage:t3.xlarge
- **Description:** $0.1824 per On Demand Linux t3.xlarge Instance Hour

### MyThirdInstance

- **Hourly price:** $0.0912000000 Hrs
- **Usage Type:** EU-BoxUsage:t3.large
- **Description:** $0.0912 per On Demand Linux t3.large Instance Hour

### firstTaskDef

- **Hourly price:** $0.01234 Hrs
- **Usage Type:** Fargate-vCPU-Hours:256
- **Description:** Fargate 256CPU/512Memory

</details>

---

## Getting Started

**Step 1: Install CloudBurn**

[![Install CloudBurn](https://img.shields.io/badge/Install-CloudBurn-blue?logo=github)](https://github.com/marketplace/cloudburn-io)

Click "Install" and select the repositories where you manage AWS infrastructure.

**Step 2: Install the GitHub Action**

CloudBurn needs your infrastructure diff/plan output to calculate costs. Install the companion action for your tool:

- **Terraform:** [Terraform Plan PR Commenter](https://github.com/marketplace/actions/terraform-plan-pr-commenter) ([docs](https://cloudburn.io/docs/terraform-plan-github-action))
- **AWS CDK:** [AWS CDK Diff PR Commenter](https://github.com/marketplace/actions/aws-cdk-diff-pr-commenter) ([docs](https://cloudburn.io/docs/aws-cdk-diff-github-action))

These actions post your `terraform plan` or `cdk diff` output as a PR comment, which CloudBurn then analyzes.

**Step 3: Create a Pull Request**

Open a PR with infrastructure changes and CloudBurn automatically posts cost analysis within seconds.

## How It Works

1. You open a PR with Terraform or CDK changes
2. GitHub Action posts the infrastructure diff/plan as a comment
3. CloudBurn detects the diff, analyzes it using real-time AWS pricing
4. Cost report appears in your PR showing exactly what each change costs

## Pricing

**Community (Free)**
- 1 repository
- Unlimited users
- Perfect for individual developers and open-source projects

**Pro Plans** (14-day free trial)
- **Pro Starter**: 5 repos - $29/month
- **Pro Team**: 10 repos - $49/month (Most Popular)
- **Pro Business**: 25 repos - $99/month
- **Pro Enterprise**: Unlimited repos - $199/month

[View Full Pricing](https://github.com/marketplace/cloudburn-io)

## Documentation & Support

**Documentation:**
- [Installation Guide](https://cloudburn.io/docs/install)
- [AWS CDK Setup](https://cloudburn.io/docs/aws-cdk-diff-github-action)
- [Terraform Setup](https://cloudburn.io/docs/terraform-plan-github-action)

**Community:**
- [Product Roadmap](https://roadmap.cloudburn.io) - Vote on features
- [Discussions](https://github.com/towardsthecloud/cloudburn.io/discussions/categories/general)
- [Report Issues](https://github.com/towardsthecloud/cloudburn.io/issues)

**Support:**
- Community: GitHub Issues
- Pro Plans: Email support (priority for Team/Business/Enterprise)
