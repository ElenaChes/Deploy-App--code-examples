# Dockerfile examples

Examples of working Dockerfiles.<br>
These Dockerfiles have been used for Node JS apps, so be mindful when adjusting them for different languages.

> [!WARNING]
> The files in this folder have distinct names for easier referencing so make sure that your file is simply named `Dockerfile` without any additions.

> [!NOTE]
> Note that the examples expose port 8080, as my apps tend to have a web interface and listen to that port.<br>
> Remove the line `EXPOSE 8080` if irrelevant.

<details>

  <summary><h3>Content</h3></summary>

- [Dockerfile_generic](#dockerfile_generic)
- [Dockerfile_puppeteer](#dockerfile_puppeteer)
- [.dockerignore](#dockerignore)

</details>
<hr>

# Dockerfile_generic

The file I use for most apps, for example:

- Express JS web apps
- Discord bots
- REST APIs

# Dockerfile_puppeteer

One of my projects used [puppeteer-html-pdf](https://www.npmjs.com/package/puppeteer-html-pdf), for the app to work in production it needed access to chromium and other Puppeteer's requirements to be installed in a specific order, so this is an adjusted file that worked for me.<br>

> [!NOTE]
> This Dockerfile includes a broader set of dependencies, which you can adjust based on your specific Puppeteer needs.

Additionally, my project had a file at the root of my project called `.puppeteerrc.cjs`, containing the following code:

```
const {join} = require('path');

/**
 * @type {import("puppeteer").Configuration}
 */
module.exports = {
  // Changes the cache location for Puppeteer.
  cacheDirectory: join(__dirname, '.cache', 'puppeteer'),
};
```

# .dockerignore

Usually a `.dockerignore` file will have the same content as your `.gitignore` file, so for Node JS the following tends to be enough:

```
.env
node_modules/
```

Feel free to check out the [.dockerignore files documentation](https://docs.docker.com/build/concepts/context/#dockerignore-files).
