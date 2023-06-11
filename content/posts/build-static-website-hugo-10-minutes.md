---
title: "🌐 How to Build a Static Website with Hugo in Under Ten Minutes: A Step-by-Step Guide"
date: 2023-06-11
showToc: true
tags: ["hugo", "static website", "github", "CI/CD pipeline", "Hugo tutorial", "Hugo website"]
---

Discover how to showcase your work using Hugo, a powerful tool that integrates `markdown` files with a CI/CD pipeline, minimizing the time needed to build a professional-looking website.

# 🎯 Project Objectives
1. Learn how to build a Hugo website in under ten minutes.
2. Understand the process of setting up a CI/CD pipeline in just another ten minutes.

# Necessary Tools
- `homebrew`; installation instructions can be found [here](https://brew.sh/).
- A Hugo theme; you can choose from a wide variety [here](https://themes.gohugo.io/). For this tutorial, we'll use the `PaperMod` theme from [adityatelange](git@github.com:adityatelange/hugo-PaperMod.git), which embodies simplicity and minimalism.

# 🏗️ Basic Hugo Setup Procedure
1. Install `hugo`.

```bash
brew install hugo
```

2. Create a `hugo` website.
```
hugo new site personal-website -f yml
```
I prefer using the `yml` configs because they have linting available within Microsoft VS Code.

3. Install your theme
```
# Jump into directory
cd personal-website

# Add theme as a submodule
git submodule add https://github.com/nanxiaobei/hugo-paper themes/paper
```

4. Update your `yaml` config. Your directory should look something like the below but if not, change the `hugo.toml` to `hugo.yaml`.
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

`hugo.yaml` config
```
languageCode: en-us
baseURL: ''
title:
theme: paper
```

5. Run `hugo server -D` to render the website (it should be hosted on `localhost:1313`).
6. You should have something that looks like this:
![Plain Hugo website](/build-static-website-hugo-10-minutes/hugo-plain.png#center)
*Plain blog built with **Hugo***

# ⚙️ Configuration
There are parameters available to use within the `params` of the `hugo.yaml`. They can be found [here](https://gohugo.io/getting-started/configuration/).

## ➕ Adding a new page
- Adding a new page is simple as, for example using `content/projects` will create a new `markdown` file called `projects.md` within the folder `content` as per the template found within the `archetypes/default.md` file.
- Editing the `projects.md` will reflect the changes within the browser upon saving.
```
# hugo new <folder_name>
hugo new content/projects
```

# 🔄 Implementing CI/CD with Github Actions
> To take this another level further, you can automate the update of your website using the following Github actions file.
Refer to this [CI/CD pipeline guide](https://gohugo.io/hosting-and-deployment/hosting-on-github/) from `Hugo`.
