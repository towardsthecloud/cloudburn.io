# CloudBurn

[![Install from GitHub Marketplace](https://img.shields.io/badge/Install-GitHub%20Marketplace-blue?logo=github)](https://github.com/marketplace/cloudburn-io)
[![Documentation](https://img.shields.io/badge/Docs-cloudburn.io-brightgreen)](https://cloudburn.io/docs)
[![Roadmap](https://img.shields.io/badge/Roadmap-View-orange)](https://roadmap.cloudburn.io)

**A GitHub App that automatically posts AWS cost impacts in your pull requests.**

When you write Terraform or AWS CDK code, CloudBurn analyzes the infrastructure diff and shows you exactly what it will cost before merging and deploying to production. No more discovering expensive decisions weeks later on your AWS bill when changes require production downtime and cross-team coordination.

Some of the included features:

- **Automatic cost analysis** - CloudBurn comments on every PR with infrastructure changes, showing monthly cost deltas
- **Real-time AWS pricing** - Accurate costs based on your infrastructure's region using live AWS Pricing API data
- **Detailed breakdowns** - See old vs. new monthly costs per resource with usage types and pricing details
- **Cost awareness** - Team learns AWS pricing through daily exposure, preventing expensive mistakes

## How It Works

1. **You create a PR** with infrastructure changes (Terraform or AWS CDK)
2. **GitHub Action runs** and posts the infrastructure diff/plan as a comment
3. **CloudBurn analyzes** the diff and calculates cost estimates using real-time AWS pricing
4. **Cost analysis appears** in your PR within seconds (see example output below), showing:
   - Resources being added/modified/deleted
   - Detailed cost breakdowns showing old vs. new monthly costs with delta calculations
   - Regional pricing specific to your infrastructure
   - Only relevant resources (zero-cost resources filtered out)

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

## Quick Start

### Installation (3 Steps)

**1. Install the Companion GitHub Action**

CloudBurn analyzes the infrastructure diff output to calculate costs. In order to do that you need a GitHub Action that posts your Terraform plan or CDK diff as a PR comment first. We've created and published free companion actions on the GitHub Marketplace that do exactly this.

Choose the action based on your Infrastructure-as-Code tool, then add it to your workflow:

#### For Terraform Projects

Use the [Terraform Plan PR Commenter Action](https://github.com/marketplace/actions/terraform-plan-pr-commenter) - See [full documentation](https://cloudburn.io/docs/terraform-plan-github-action) for details.

Example workflow showing where to add the action:

```yaml
name: Terraform Plan
on:
  pull_request:
    branches: [main]

jobs:
  terraform-plan:
    runs-on: ubuntu-latest
    permissions:
      pull-requests: write
      id-token: write
      contents: read

    steps:
      - uses: actions/checkout@v4

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          role-to-assume: arn:aws:iam::123456789012:role/github-actions
          aws-region: us-east-1

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v3
        with:
          terraform_version: '1.5.0'

      - name: Terraform Init
        run: terraform init

      # Add this action to your workflow ↓
      - name: Terraform Plan PR Commenter
        uses: towardsthecloud/terraform-plan-pr-commenter@v1
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
```

#### For AWS CDK Projects

Use the [AWS CDK Diff PR Commenter Action](https://github.com/marketplace/actions/aws-cdk-diff-pr-commenter) - See [full documentation](https://cloudburn.io/docs/aws-cdk-diff-github-action) for details.

Example workflow showing where to add the action:

```yaml
name: CDK Diff
on:
  pull_request:
    branches: [main]

jobs:
  cdk-diff:
    runs-on: ubuntu-latest
    permissions:
      pull-requests: write
      id-token: write
      contents: read

    steps:
      - uses: actions/checkout@v4

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          role-to-assume: arn:aws:iam::123456789012:role/github-actions
          aws-region: us-east-1

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Install dependencies
        run: npm ci

      # Add this action to your workflow ↓
      - name: CDK Diff PR Commenter
        uses: towardsthecloud/aws-cdk-diff-action@v1
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
```

**2. Install the CloudBurn App from the GitHub Marketplace**

[![Install CloudBurn](https://img.shields.io/badge/Install-CloudBurn-blue?logo=github)](https://github.com/marketplace/cloudburn-io)

**3. Open a Pull Request**

CloudBurn automatically adds cost analysis within seconds when you create a PR with infrastructure changes.

## Pricing

### Community (Free)
- Perfect for individual developers and open-source projects
- 1 repository
- Unlimited users

### Pro Plans
Starting at **$29/month** with 14-day free trial:
- Pro Starter: 5 private repos
- Pro Team: 10 private repos (Most Popular)
- Pro Business: 25 private repos
- Pro Enterprise: Unlimited repos

[View Full Pricing](https://github.com/marketplace/cloudburn-io)


## Navigation

### Documentation
- [Installation Guide](https://cloudburn.io/docs/install)
- [AWS CDK GitHub Action Docs](https://cloudburn.io/docs/aws-cdk-diff-github-action)
- [Terraform GitHub Action Docs](https://cloudburn.io/docs/terraform-plan-github-action)
- [Full Documentation](https://cloudburn.io/docs)

### Community & Support
- [Product Roadmap](https://roadmap.cloudburn.io) - Vote on upcoming features
- [Blog & Discussions](https://github.com/towardsthecloud/cloudburn.io/discussions/categories/general) - Blog comments powered by [giscus](https://giscus.app)
- [Report Issues](https://github.com/towardsthecloud/cloudburn.io/issues)

### Resources
- [Website](https://cloudburn.io)
- [GitHub Marketplace](https://github.com/marketplace/cloudburn-io)

## Support

- **Community Plan**: Community support via GitHub Issues
- **Pro Plans**: Email support (priority for Team/Business/Enterprise tiers)
