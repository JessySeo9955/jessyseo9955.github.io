---
layout: post
title:  "[DevOps] MonoRepo CI/CD Architecture"
date:   2025-05-17 20:27:14 -0400
categories: jekyll update
---

## CI/CD Architecture
### Github Actions
- [Mono Repository](https://github.com/JessySeo9955/school_angular_nest/actions)
	- Pull Request Trigger
	- Unit Tests
	- Docker Build
	- Docker Image Save to Docker Hub
	- Heroku Deployment
	- Trigger Cypress Tests in E2E Repository (Gtihub API)
- [cypress repository](https://github.com/JessySeo9955/cypress_automation/blob/main/.github/workflows/dispatch_cypress.yml)
	- Run E2E Tests  (Gtihub API)
	- Integrate with Cypress Cloud

![Architecture]( {{ '/assets/imgs/school_enrollment.drawio.png' | relative_url }} )