# Deploy App: code examples

<p>
  <img src="https://img.shields.io/badge/Node.js-grey?logo=node.js">
  <img src="https://img.shields.io/badge/Docker-grey?logo=docker">
  <img src="https://img.shields.io/badge/Fly.io-grey?logo=flydotio">
  <img src="https://img.shields.io/badge/🔬-Example_Files-grey?labelColor=lightgrey">
</p>

A comprehensive guide on deploying and setting up CI/CD (Continuous Integration & Continuous Delivery) for a Node.js app on [Fly.io](https://fly.io/).<br>
Includes a step-by-step guide, working `Dockerfiles`, and Fly.io configuration examples.

> [!NOTE]
> While these files were written and are used specifically for Node.js apps and for deploying specifically on fly.io, they can serve as an example or template for other types of apps and hosting services too.

<details>

  <summary><h3>Content</h3></summary>

- [Dockerfile Examples](Dockerfile%20examples)
  - [Dockerfile_generic](Dockerfile%20examples#dockerfile_generic)
  - [Dockerfile_puppeteer](Dockerfile%20examples#dockerfile_puppeteer)
  - [.dockerignore](Dockerfile%20examples#dockerignore)
- [Deploying on Fly.io](Deploying%20on%20Fly.io)
  - [Installing flyctl](Deploying%20on%20Fly.io#installing-flyctl)
  - [Launching on Fly.io](Deploying%20on%20Fly.io#launching-on-flyio)
    - [Secrets](Deploying%20on%20Fly.io#secrets)
    - [fly.toml](Deploying%20on%20Fly.io#flytoml)
  - [Continuous Deployment on Fly.io](Deploying%20on%20Fly.io#continuous-deployment-on-flyio)
    - [Get a Fly Token](Deploying%20on%20Fly.io#get-a-fly-token)
    - [Github Actions](Deploying%20on%20Fly.io#github-actions)
    - [fly.yml](Deploying%20on%20Fly.io#flyyml)
  - [More Relevant Documentation](Deploying%20on%20Fly.io#more-relevant-documentation)
- [App Structure](#appstructure)

</details>
<hr>

# Docker Examples

Contains working `Dockerfiles` examples with context on the types of apps they're typically used for.<br>
([Go to readme](Dockerfile%20examples))

# Deploying on fly.io

Step-by-step description of the process, from deciding to deploy an app on Fly.io to having a live deployment, alongside an explanation of setting up CI/CD using GitHub Actions.<br>
Also contains examples of working `fly.toml` and `fly.yml` files and explanations of their contents.<br>
([Go to readme](Deploying%20on%20Fly.io))

# App Structure

Here's a visual representation of how a structure using these file examples would look in an actual Node.js app:

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
