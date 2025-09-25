# Deploy App: code examples

A comprehensive guide on deploying and setting up CI/CD (Continuous Integration & Continuous Delivery) for a Node JS app on [Fly.io](https://fly.io/).<br>
Description: includes a step by step guide, along with Dockerfile and Fly.io configuration example files.

> [!NOTE]
> While these files were written and are used specifically for Node JS apps and for deploying specifically on fly.io, they can serve as an example or template for other types of apps and hosting services too.

<details>

  <summary><h3>Content</h3></summary>

- [Dockerfile examples](/Dockerfile%20examples)
  - [Dockerfile_generic](/Dockerfile%20examples#dockerfile_generic)
  - [Dockerfile_puppeteer](/Dockerfile%20examples#dockerfile_puppeteer)
  - [.dockerignore](/Dockerfile%20examples#dockerignore)
- [Deploying on Fly.io](/Deploying%20on%20Fly.io)
  - [Installing flyctl](/Deploying%20on%20Fly.io#installing-flyctl)
  - [Launching on Fly.io](/Deploying%20on%20Fly.io#launching-on-flyio)
    - [Secrets](/Deploying%20on%20Fly.io#secrets)
    - [fly.toml](/Deploying%20on%20Fly.io#flytoml)
  - [Continuous deployment on Fly.io](/Deploying%20on%20Fly.io#continuous-deployment-on-flyio)
    - [Get a fly token](/Deploying%20on%20Fly.io#get-a-fly-token)
    - [Github actions](/Deploying%20on%20Fly.io#github-actions)
    - [fly.yml](/Deploying%20on%20Fly.io#flyyml)
  - [More relevant documentation](/Deploying%20on%20Fly.io#more-relevant-documentation)
- [App structure](#appstructure)

</details>
<hr>

# Docker examples

Contains examples of working `Dockerfiles` and some context on what type of apps they're used by.<br>
([Go to readme](/Dockerfile%20examples))

# Deploying on fly.io

Step by step description of the process from deciding to deploy an app on Fly.io and to having a deployed app, alongside an explanation on setting up CI/CD using Github actions.<br>
Also contains examples of working `fly.toml` and `fly.yml` files and explanations of their contents.<br>
([Go to readme](/Deploying%20on%20Fly.io))

# App structure

Here's a visual representation of how a structure using these file examples would look in an actual Node JS app:

```
app/
├── .github/
│   └── workflows/
│       └── fly.yml
├── node_modules/
├── .dockerignore
├── .gitignore
├── Dockerfile
├── fly.toml
├── index.js
├── package-lock.json
├── package.json
```
