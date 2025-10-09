# Deploying on Fly.io

Step-by-step guide for deploying an app on [Fly.io](https://fly.io/) and setting up CI/CD with GitHub Actions.

<details>

  <summary><h3>Content</h3></summary>

- [Installing flyctl](#installing-flyctl)
- [Launching on Fly.io](#launching-on-flyio)
  - [Secrets](#secrets)
  - [fly.toml](#flytoml)
- [Continuous Deployment on Fly.io](#continuous-deployment-on-flyio)
  - [Get a Fly Token](#get-a-fly-token)
  - [Github Actions](#github-actions)
  - [fly.yml](#flyyml)
- [More Relevant Documentation](#more-relevant-documentation)
  - [Environment Variables](#environment-variables)
  - [Fly.io](#flyio)
  - [GitHub](#github)

</details>
<hr>

# Installing flyctl

To deploy apps on Fly.io, you need to install their command-line utility, `flyctl`.<br>
For example, on `Windows` open PowerShell and run:

```
pwsh -Command "iwr https://fly.io/install.ps1 -useb | iex"
```

For other operating systems you can check their documentation here: [Install flyctl](https://fly.io/docs/flyctl/install/).<br>
Make sure to register on Fly.io and log in to your account via the command-line.

# Launching on Fly.io

> [!NOTE]
> If you prefer, you can follow Fly.io's documentation of the process instead: [Create an app with Fly Launch](https://fly.io/docs/launch/create/), then skip to the [fly.toml](#flytoml) section.

1. Select or create a `Dockerfile` and `.dockerignore` that fit your app, and add them to the root of your project.
2. Run the following command in a terminal to create the app on Fly.io and deploy it in one go:

```
fly launch
```

Alternatively if you'd like to check your configuration before you deploy, you can run:

```
fly launch --no-deploy
```

1. Fill out the prompts in the terminal, and your app will be deployed.

> [!WARNING]
> By default, Fly apps are initialized with 2 machines, which may not be necessary and could increase costs.<br>
> To switch to a single machine, run `fly scale 1`.

## Secrets

Store sensitive information, such as tokens or passwords, as environment variables. On Fly.io and many other hosting services, these are referred to as **Secrets**.

You can set your secrets one by one using the following command, while `VARNAME` is the name of the variable, and `VARVALUE` is its value:

```
fly secrets set VARNAME=VARVALUE
```

> [!NOTE]
> Fly.io seems to be adding more options to their web interface and it's now possible to set new environment variables in the `Secrets` tab inside the app's page.

## fly.toml

Fly generates a `fly.toml` configuration file when you launch a new app. You may need to adjust it if your app has different requirements.<br>
The attached `fly.toml` file is one I use for Node.js apps with a web interface, these configurations tell Fly.io to:

- Use `Dockerfile` and `.dockerignore` files to build the app.

```toml
[build]
  dockerfile = "Dockerfile"
  ignorefile = "dockerignore"
```

> [!TIP]
> While you can build using prebuilt images, Node.js images often consume more RAM than desired and may fail to launch in some cases. Using a Dockerfile avoids these issues and is straightforward once set up.

- Open port 8080, which the app listens to on launch. You can change this to any port your app requires.

```toml
[[services]]
  #...
  internal_port = 8080
```

- Give the app a 1 minute grace period. Fly waits this long before performing health checks on the app. You can adjust this for faster apps.

```toml
[[services]]
  #...
  [[services.tcp_checks]]
    #...
    grace_period = "1m0s"
```

- Uses a swap size of 512mb, adjust based on your needs or remove completely if not using memory swap.

```toml
swap_size_mb = 512
```

For these configurations to work, I also have the following in my `package.json`:

```json
  "dockerfile": {
    "port": 8080,
    "swap": "512M"
  }
```

> [!IMPORTANT]
> If you're using a Dockerfile that relies on `package-lock.json`, make sure to remove the file from your `.dockerignore` and `.gitignore` as launching will fail otherwise.

# Continuous Deployment on Fly.io

> [!NOTE]
> You can follow the official documentation of the process: [Continuous Deployment with Fly.io and GitHub Actions](https://fly.io/docs/launch/continuous-deployment-with-github-actions/), then skip to the [fly.yml](#flyyml) section.

## Get a Fly Token

1. Assuming you already have the app on Fly.io - simply run the following:

```
fly tokens create deploy -x 999999h
```

The output you get is your app's token and will be needed in a moment, make sure to keep it secret as it's essentially a "password" for your app.

## Github Actions

1. Go to the settings of your repository.
2. Open `Secrets and variables` on the sidebar and go to `Actions`.
3. Click `New repository secret`:
   - Name the secret, we're going to follow the guide and call it `FLY_API_TOKEN`.
   - Paste the token you got from fly into the Secret section.

## fly.yml

1. Create a folder in the root of your project called `.github`.
2. Inside `.github` create another folder called `workflows`.
3. Place `fly.yml` inside of `workflows`.
   - If you'd like your Github repository to automatically update the environment it's running (in the Deployments section), add the following lines in `fly.yml` under the `deploy` category, while `APPNAME` is the name you want the environment to have, and `APPURL` is the app's URL (if it has one):

```
deploy:
  ...
  environment:
    name: APPNAME
    url: APPURL
steps:
  ...
```

After pushing code to GitHub (or creating a new release), the app will automatically redeploy on Fly.io.

> [!TIP]
> To redeploy only on pushes to the `main` or `master` branch, adjust the `on` action in `fly.yml` to specify the branch. Alternatively, push to `main`/`master` and add `.github` to the `.gitignore` file to prevent the workflow from running on other branches.

# More Relevant Documentation

## Environment Variables

- [How to read environment variables from Node.js](https://nodejs.org/en/learn/command-line/how-to-read-environment-variables-from-nodejs)
- [dotenv module](https://www.npmjs.com/package/dotenv)

## Fly.io

- [Get app info](https://fly.io/docs/apps/info/)
- [Deploy an app](https://fly.io/docs/launch/deploy/) - `fly deploy` (redeploy an app you already launched, updates its code)
- [Restart apps or Machines](https://fly.io/docs/apps/restart/) - `fly apps restart APPNAME`/`fly machine restart MACHINEID` (restart the app without changing its code)
- [Set secrets](https://fly.io/docs/apps/secrets/)
- [Scale Machine CPU and RAM](https://fly.io/docs/launch/scale-machine/)
- [Grace period](https://fly.io/docs/getting-started/troubleshooting/#grace-period)
- [Delete an app](https://fly.io/docs/apps/delete/) - `fly apps destroy APPNAME`

## GitHub

- [Understanding GitHub Actions](https://docs.github.com/en/actions/about-github-actions/understanding-github-actions)
- [Using secrets in Github Actions](https://docs.github.com/en/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions)
