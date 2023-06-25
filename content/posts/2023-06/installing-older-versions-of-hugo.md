---
title: "❄️ Installing Older Versions of `hugo`"
date: 2023-06-30
tags: ["hugo", "static website", "github", "Hugo tutorial", "Hugo website"]
---

Installing a previous version of `hugo` via `brew` is not as easy as installing the latest version.

## Steps
1. Clone the latest repository of the software that you require. I need an older version of `hugo` and it uses `go` so I will be building that from source.

```
git clone git@github.com:gohugoio/hugo.git
```

2. Navigate to the directory
```
cd hugo
```

3. Checkout to the version of `hugo` that you require e.g. version `v0.113.0` is at `SHA5` of `085c1b3d614e23d218ebf9daad909deaa2390c9a`.

```
hugo checkout 085c1b3d614e23d218ebf9daad909deaa2390c9a
```

4. Install `go` and build the package
```
# install go
brew install go

# build package from source
go build
```

5. Copy `hugo` file to your `PATH`
```
# On Mac
sudo cp hugo /usr/local/bin
```

6. Assert that the installed version of `hugo` is the one you require.

```
hugo version
hugo v0.113.0-085c1b3d614e23d218ebf9daad909deaa2390c9a darwin/arm6
```

7. Never touch it again.