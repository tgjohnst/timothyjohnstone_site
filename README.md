# Personal Website - [www.timothyjohnstone.com](https://www.timothyjohnstone.com).

A simple, modern, static personal website.

## Overview

This site is built as a single-page static site using [Tailwind CSS](https://tailwindcss.com/) and [Lucide Icons](https://lucide.dev/). It features a responsive design, interactive background animation, and links to professional profiles.

## Hosting Architecture

The site is hosted on AWS using the following architecture:

- **Amazon S3**: The site files are stored in an S3 bucket configured for static website hosting.
- **Amazon CloudFront**: A CloudFront distribution provides global CDN caching and HTTPS support.
- **Amazon Route 53**: Domain management and DNS routing are handled via Route 53.
- **AWS Certificate Manager (ACM)**: SSL/TLS certificates for HTTPS are provisioned and managed via ACM.

### Deployment Workflow

Automated deployment is handled via [GitHub Actions](https://github.com/features/actions):

- On every push to the `main` branch, the workflow defined in [`.github/workflows/main.yml`](.github/workflows/main.yml) runs.
- The workflow:
  1. Checks out the repository.
  2. Configures AWS credentials using GitHub secrets and repository variables.
  3. Syncs the contents of the [`public/`](public/index.html) directory to the target S3 bucket, deleting any removed files.

### AWS Setup Details
A few notes, in case you want to replicate this setup:

- **S3 Bucket**: Must be configured for static website hosting. The bucket name is set via the `AWS_S3_TARGET_BUCKET_NAME` variable in the Actions automation.
- **CloudFront**: The distribution should point to the S3 bucket as its origin. Make sure to set up an alternate domain name (CNAME) and attach the ACM certificate.
- **Route 53**: Create an A/AAAA record pointing your domain to the CloudFront distribution, or have these managed by CF itself.
- **ACM**: Request a wildcard certificate for your domain and validate it via DNS in Route 53.

## Local Development

To preview or edit the site locally:

1. Open [`public/index.html`](public/index.html) in your browser.
2. Edit files in the `public/` directory as needed.
3. Commit and push changes to `main` to trigger deployment.

## Repository Structure

```
README.md
.github/
  workflows/
    main.yml         # GitHub Actions deployment workflow
public/
  index.html         # Main site HTML
  assets/            # Images and other static assets
```

---

**Hosted on AWS, automated by GitHub Actions.**