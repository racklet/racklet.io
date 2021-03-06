# racklet.io

This repo houses the assets used to build the Racklet project's landing page at https://racklet.io.

> **Note**: The sources for an individual Racklet project's (e.g. `racklet/racklet`) documentation at https://docs.racklet.io are housed in its respective Racklet repo (e.g. https://github.com/racklet/racklet). Issues and pull requests for a specific project's documentation should be registered in its own repo.

## Note on the origin of this website

This website repo is forked from the excellent https://github.com/fluxcd/website repository hosting the very nice https://fluxcd.io website.

Instead of reinventing the wheel, we figured we'd use the same website template over time (Racklet is also Apache 2.0-licensed). As time passes, we expect to diverge more and more from the original website template (intentionally) to not confuse readers with two website UIs that look the same.

However, if there is some nice feature we can upstream, we are most happy to do so!

Thanks a lot to the maintainers of the `fluxcd/website` project, listed here for attribution:

```txt
Daniel Holbach, Weaveworks <daniel@weave.works> (GitHub: @dholbach, Slack: dholbach)
Hidde Beydals, Weaveworks <hidde@weave.works> (GitHub: @hiddeco, Slack: hidde)
Scott Rigby, Weaveworks <scott@weave.works> (GitHub: @scottrigby, Slack: scottrigby)
```

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
