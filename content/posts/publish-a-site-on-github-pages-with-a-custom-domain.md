+++
title = "Publish a Site on Github Pages with a Custom Domain"
date = "2022-12-30T13:08:50-06:00"
author = "Cron Quixote"
authorTwitter = "" #do not include @
cover = ""
tags = ["github-pages"]
keywords = ["", ""]
description = "Learn how to publish a site to GitHub Pages using a custom domain."
showFullContent = false
readingTime = false
hideComments = false
color = "" #color from the theme settings
ToC = true
+++

## Preface
All the information needed to do this is present in the official docs, however:
- The content is spread across many pages
- Each page contains a lot of content irrelevant to this use case
- The docs are largely beginner-focused

This post is a streamlined and somewhat-opinionated guide for experienced engineers.

## 1. Publish a simple "Hello, World!" page
[Official docs](https://pages.github.com/)

Create a new public repo with the required naming convention: `<username>.github.io`.

Add an `index.html` file to this repo with any content, e.g. `Hello, World!`.

Visit `https://<username>.github.io` to verify that it serves the `index.html` file you just created.

## 2. Configure your custom domain on GitHub
[Official docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain)

Visit your new repo in GitHub and click the "Settings" button.

In the left sidebar, click "Pages".

In the "Custom Domain" input, enter your domain, e.g. `example.com`.

When you do this, GitHub adds a `CNAME` file to your repository root, whose content is just the domain you entered above.

Because of this file addition, sync your local repo with the remote before making any additional changes.

## 3. Configure your custom domain on your DNS provider
[Official docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain)

Remove any existing DNS records you don't need.

Add four A records for the root domain so that it points to the GitHub pages IPs:
|Record Type|Host|Value|
|-----------|----|-----|
|A|@|185.199.108.153|
|A|@|185.199.109.153|
|A|@|185.199.110.153|
|A|@|185.199.111.153|

You can optionally add AAAA records for IPv6.

Add a CNAME record to redirect the `www.` subdomain to your root domain:
|Record Type|Host|Value|
|-----------|----|-----|
|CNAME|www.example.com.|example.com|

## 4. Verify that your custom domain works
[Official docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/troubleshooting-custom-domains-and-github-pages)

Visit your custom domain and ensure that it serves your `index.html` file. If not, follow the troubleshooting steps linked above.

## 5. Decide how you want to build your site
[Official docs for Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll)

[Official docs for other static site generators](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#static-site-generators)

You have two options for building your site:
1. Locally
2. Remotely (on GitHub)

I recommend building locally. You're going to want to test your site locally anyway, so why not build it there and skip dealing with GitHub-specific quirks, limitations, and configurations?

If you choose to build remotely and you use Jekyll as a static site generator, the build process will be automatic. Otherwise, you'll need to configure GitHub Actions to build your site.
## 6. Build your initial site and push it
Set up your chosen static site generator locally and run your first build, placing the built files in your site repo's root.

Before pushing the built files to GitHub, ensure that the `CNAME` file created above is present in the repository root.

Push the files and verify that your built site is served at your custom domain.

## 7. Mission accomplished
Now it's time to get writing! 🎉

## Optional: Secure your custom domain on GitHub to prevent potential takeovers
[Offical docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages)

Note: This is only a risk if your domain's DNS records point to GitHub Pages but your site is misconfigured on GitHub or its repo is deleted.

## Optional: Change your publishing directory
[Official docs](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

You can change the directory that GitHub uses to serve your site. GitHub calls this directory a "publishing source".

It can be one of the following:
1. The root
2. The `docs/` subdirectory

You cannot set your publishing source to an arbitrary subdirectory.

The advantage of using the `docs/` subdirectory is that you can use the root directory to store files that you want to store in the repo, but don't want to be served with the site, e.g. a `README` file.

To change the publishing source, visit the "Pages" section of your repo's settings and modify the "Source" dropdown. You can also change the branch that GitHub uses to publish your site to something other than `main`.

Note that if you change your publishing source to the `docs/` subdirectory, then the `CNAME` file must exist in that subdirectory, not the repo root.

