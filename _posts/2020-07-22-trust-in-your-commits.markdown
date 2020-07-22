---
title: Trust In Your Commits
date: 2020-07-22 11:17:00 -06:00
categories:
    - go
tags:
    - git
    - go
---

Recently I've been working on a new _Go_ project, it must be shared across the team, and I wanted to be sure that all of the test passed and have a `goimports` and `golint` run everytime before a commit, just to have that pretty code and follow some standards.

I know this can be done with [git hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks), but since the content of these need to be inside of the `.git` folder, it'll be hard to share across the repository and the team, and later if you want to make some changes on the hooks, it gets even harder!

I came across with [pre-commit](https://pre-commit.com/), an awesome framework that helps you manage and maintain multi-language pre-commit hooks. It is fairly easy too install, works with _Go_ out of the box, and once you have your configuration set in your `.pre-commit-config.yaml`, you just have to add it to your repo and just tell your team to [install pre-commit](https://pre-commit.com/#install) and run `pre-commit install` on their project. That's it! Every time they `commit` to the repo the hooks that are set on the configuration file will be run.

The good thing about this framework is that it get the hooks from remote repositories, you don't have to install anything or whatnot, so at the end the `.pre-commit-config.yaml` acts pretty much like a _mod_ file.

You can find multiple repositories that contain pretty good hooks for _Go_ ready for `pre-commit`. My favorites are:

-   [https://github.com/dnephin/pre-commit-golang](https://github.com/dnephin/pre-commit-golang)
-   [https://github.com/Bahjat/pre-commit-golang](https://github.com/Bahjat/pre-commit-golang)
-   [https://github.com/TekWizely/pre-commit-golang#go-fmt](https://github.com/TekWizely/pre-commit-golang#go-fmt)

You can decide which hooks to run from which repository, it's up to you. For example, I run hooks from two different because the one for unit tests does a better job on _Bahjat_ repository.

This is the `.pre-commit-config.yaml` that I'm currently using:

```
repos:
  - repo: git://github.com/dnephin/pre-commit-golang
    rev: master
    hooks:
      - id: go-imports
  - repo: git://github.com/Bahjat/pre-commit-golang
    rev: master
    hooks:
      - id: go-lint
      - id: go-unit-tests
```

Feel free to grab it use it in your own projects, it works pretty fine for me!
