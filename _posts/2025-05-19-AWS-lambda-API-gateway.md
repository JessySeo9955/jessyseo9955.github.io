---
layout: post
title:  "[DevOps|Back-end] Weather Compare - AWS Lambda, API Gateway, FatJar"
date:   2025-05-19 20:27:14 -0400
categories: jekyll update
---


## Project
- [[Repository] Weather Compare Serverless Rest API](https://github.com/JessySeo9955/indexedDB_weather_backend)
- Java, Gradle, FatJar, AWS Lambda, AWS Gateway
- Junit

## Architecture flowchart
<img style="max-width: 100%; border: 1px solid #ddd" src="assets/imgs/weather_backend.png" />

## CI/CD & Hosting

- GitHub Actions – for automated build and deployment workflows
- Firebase Hosting – for static site hosting




## References
- [API Gateway VS Load Balancer](#reference1)
- [API Gateway HTTP API VS  REST API](#reference2)
- [Fat JAR vs AWS Lambda Layer](#reference3)



<div id="reference1">

##  API Gateway VS Load Balancer

API Gateway is tailored for API management, serverless applications, and advanced API features (like security, rate limiting, etc.), while Load Balancers are more focused on distributing traffic to backend servers, typically for traditional web applications or microservices that are server-based (EC2, ECS).

| Feature | **API Gateway** | **Load Balancer** (ALB/NLB) |
| --------|-----------------|-----------------------------|
| **Purpose** | Manage and expose APIs | Distribute traffic across servers or instances |
| **Protocols Supported** | HTTP/S, WebSocket | HTTP/S, TCP, UDP (ALB, NLB) |
| **Serverless Support** | Deep integration with AWS Lambda | Not typically serverless-focused |
 

</div>

<div id="reference2">

##  API Gateway HTTP API VS  REST API

- HTTP API (newer, simpler, cheaper)
- REST API (older, more powerful, more expensive)

### Summary of Differences:

| Feature | **HTTP API** (Recommended for most new projects) | **REST API** (Advanced use cases) |
| --- | --- | --- |
| **Pricing** | ✅ Cheaper (up to 70% less) | ❌ More expensive |
| **Performance** | ✅ Lower latency | ❌ Slightly higher latency |
| **Ease of Use** | ✅ Simpler, faster setup | ❌ More complex setup |
| **Features** | ❌ Fewer features | ✅ More features (e.g., request/response mapping) |
| **Authorization** | ✅ IAM, JWT (Cognito), Lambda authorizers | ✅ IAM, Cognito, Lambda authorizers |
| **Custom Domain Support** | ✅ Yes | ✅ Yes |
| **WebSockets Support** | ❌ No | ✅ Yes |
| **Caching** | ❌ No | ✅ Yes |
| **API Gateway VPC Links** | ❌ No | ✅ Yes |
| **Use Case** | 💡 Basic APIs, microservices, mobile backends | 💡 Complex APIs with transformations, legacy support |

</div>

<div id="reference3">

##  Fat JAR vs AWS Lambda Layer

| Use Case | Recommended Approach |
| --- | --- |
| Simpler projects, fast iteration | ✅ Fat JAR |
| Many functions sharing dependencies | 🔄 Fat JAR + Layers |
| Enterprise-scale, optimized builds | ✅ Layers (with CI/CD) |

### Fat JAR
When you build the Fat JAR, the contents of gson-2.8.8.jar are flattened and merged directly into the root of your Fat JAR. So your Fat JAR will look something like this:
<pre>
my-application.jar
│
├── META-INF/
│   ├── MANIFEST.MF
│
├── com/                        (Your application's classes)
│   └── myapp/
│       └── Main.class
│
├── com/                        (Flattened dependency classes)
│   └── google/
│       └── gson/
│           ├── Gson.class
│           ├── JsonObject.class
│           └── ...
└── ...                         (Other dependencies)
</pre>
</div>

