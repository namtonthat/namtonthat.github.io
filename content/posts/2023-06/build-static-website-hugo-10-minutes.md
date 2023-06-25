---
title: "🌐 How to Build a Static Website with Hugo in Under Ten Minutes: A Step-by-Step Guide"
date: 2023-06-11
showToc: true
tags: ["hugo", "static website", "github", "CI/CD pipeline", "Hugo tutorial", "Hugo website"]
---

Discover how to showcase your work using Hugo, a powerful tool that integrates `markdown` files with a CI/CD pipeline, minimizing the time needed to build a professional-looking website.

## 🎯 Project Objectives
1. Learn how to build a Hugo website in under five steps.
2. Understand the process of setting up a CI/CD pipeline in just another two minutes.

## Necessary Tools
- `homebrew`; installation instructions can be found [here](https://brew.sh/).
- A Hugo theme; you can choose from a wide variety [here](https://themes.gohugo.io/). For this tutorial, we'll use the `paper` theme from [nanxiaobei](git@github.com:nanxiaobei/hugo-paper.git), which embodies simplicity and minimalism.

## 🏗️ Basic Hugo Setup Procedure
1. Install `hugo`.

```bash
brew install hugo
```

2. Create a `hugo` website.
```
hugo new site your-username.github.io -f yml
```
*Notes*
- I prefer using the `yml` configs because it gets automatically linted within VS Code.
- Using `your-username.github.io` allows you to use that as the URL when it gets published to the web.

3. Install your theme
```
# Jump into directory
cd your-username.github.io

# Add theme as a submodule
git init
git submodule add https://github.com/nanxiaobei/hugo-paper themes/paper
```

4. Update your `yaml` config.
`hugo.yaml` config
```
languageCode: en-us
baseURL: your-username.github.io
title:
theme: paper
```

5.  Create a new post
```
hugo new posts/<new_post_name>
```

Your directory should look something like the below but if not, change the `hugo.toml` to `hugo.yaml`.
```
├── archetypes
│   └── default.md
├── assets
├── content
│   └── posts
│       └── build-static-website-hugo-10-minutes.md
├── data
├── hugo.yaml
├── layouts
├── resources
│   └── _gen
│       ├── assets
│       └── images
├── static
└── themes
    └── paper
    ...
```

6. Run `hugo server -D` to render the website (it should be hosted on `localhost:1313`).
You should have something that looks like this:
![Plain Hugo website](/build-static-website-hugo-10-minutes/hugo-plain.png#center)
*Plain blog built with **Hugo***

## ⚙️ Configuration
There are parameters available to use within the `params` of the `hugo.yaml`. They can be found [here](https://gohugo.io/getting-started/configuration/).

### ➕ Adding a new page
6.  Adding a new page is simple as, for example using `content/projects` will create a new `markdown` file called `projects.md` within the folder `content` as per the template found within the `archetypes/default.md` file.

Editing the `projects.md` will reflect the changes within the browser upon saving.
```
# hugo new <folder_name>/<post_name>
hugo new content/projects
```

## 🔄 Implementing CI/CD with Github Actions
> To take this another level further, you can automate the update of your website using the following Github actions file.
- Refer to this [CI/CD pipeline guide](https://gohugo.io/hosting-and-deployment/hosting-on-github/) from `Hugo`.
1. Copy the `hugo.yaml` file from `Step 6.`
2. Run a `git push`
3. Your website should now be live.
![Live website](/build-static-website-hugo-10-minutes/live-website.png#center)
*Inception...*