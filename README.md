# racklet.io

This repo houses the assets used to build the Racklet's project's landing page at https://racklet.io.

> **Note**: The sources for Racklet's individual project's documentation (e.g. `racklet/racklet`) at https://docs.racklet.io, are housed in the respective Racklet repo (e.g. https://github.com/racklet/racklet). Issues and pull requests for specific project's documentation should be registered at that repo.

This website repo is forked from the excellent https://github.com/fluxcd/website repository hosting the very nice https://fluxcd.io website. Instead of reinventing the wheel, we figured we'd use the same website template over time. As time passes, we expect to diverge more and more from the original website template (intentionally) to not confuse readers with two website UIs that look the same. However, if there is some nice feature we can upstream, we are most happy to do so! Thanks to all the maintainers of the fluxcd/website project!

## Running the site locally

In order to run the Racklet site locally, you need to install:

* [Node.js](https://www.npmjs.com/get-npm)
* The [Hugo](https://gohugo.io) static site generator. Make sure to [install](https://gohugo.io/getting-started/installing/) the "extended" variant of Hugo with support for the [Hugo Pipes](https://gohugo.io/hugo-pipes/introduction/) feature and to check the [`netlify.toml`](./netlify.toml) configuration file for which version of Hugo you should install.

Once those tools are installed, fetch the assets necessary to run the site:

```bash
npm install
```

Then run the site in "server" mode:

```bash
make serve
```

Navigate to http://localhost:1313 to see the site running in your browser. As you make updates to the site, the browser will immediately update to reflect those changes.

## Publishing the site

The Racklet website is published automatically by [Netlify](https://netlify.com) when changes are pushed to the `main` branch. The site does not need to be published manually.

### Preview builds

When you submit a pull request to this repository, Netlify builds a "deploy preview" of your changes. You can see that preview by clicking on the **deploy/netlify** link in the pull request window.
