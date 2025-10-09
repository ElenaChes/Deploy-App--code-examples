# Dockerfile examples

Examples of working Dockerfiles.<br>
These Dockerfiles were designed for Node.js apps. Adjust them carefully if you intend to use them with other languages.

> [!WARNING]
> The files in this folder have unique names for easier reference. Make sure your actual Dockerfile is named exactly `Dockerfile` with no extra characters.

> [!NOTE]
> These examples expose port 8080, which is typical for my apps with web interfaces. Remove or change the `EXPOSE 8080` line if your app uses a different port.

<details>

  <summary><h3>Content</h3></summary>

- [Dockerfile_generic](#dockerfile_generic)
- [Dockerfile_puppeteer](#dockerfile_puppeteer)
- [.dockerignore](#dockerignore)

</details>
<hr>

# Dockerfile_generic

This is the Dockerfile I typically use for most apps, including:

- Express.js web apps
- Discord bots
- RESTful APIs

# Dockerfile_puppeteer

One of my projects used [puppeteer-html-pdf](https://www.npmjs.com/package/puppeteer-html-pdf). To run in production, the app required Chromium and other Puppeteer dependencies to be installed in a specific order. This Dockerfile reflects the adjustments that worked for me.

> [!NOTE]
> This Dockerfile includes a broader set of dependencies, which you can adjust based on your specific Puppeteer needs.

Additionally, my project had a file at the root of my project called `.puppeteerrc.cjs`, containing the following code:

```js
const { join } = require("path");

/**
 * @type {import("puppeteer").Configuration}
 */
module.exports = {
  // Changes the cache location for Puppeteer.
  cacheDirectory: join(__dirname, ".cache", "puppeteer"),
};
```

# .dockerignore

A `.dockerignore` file often mirrors your `.gitignore`. For Node.js projects, the following is usually sufficient:

```
.env
node_modules/
```

Feel free to check out the [.dockerignore files documentation](https://docs.docker.com/build/concepts/context/#dockerignore-files).
