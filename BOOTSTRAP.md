# Bootstrapping an Enterprise

A decentralized enterprise should have code in multiple online source code management (SCM) platforms. We chose:

* [codeberg.org](https://codeberg.org/), because it's ["an open community of free software enthusiasts providing a humane, non-commercial and privacy-friendly alternative to commercial services such as GitHub."](https://docs.codeberg.org/getting-started/what-is-codeberg/)
* [gitlab.com](https://gitlab.com/), because they ["been firm believers in remote work, open source, DevSecOps, and iteration."](https://about.gitlab.com/company/)
* [github.com](https://github.com/), because they're currently the most popular platform, and we want to reach as large an audience as possible.

To do this, we created these organizations/groups (TODO: use SCMs' APIs to script org creation):

* https://codeberg.org/devopscoop
* https://gitlab.com/devopscoop
* https://github.com/devopscoop

Then created this `enterprise` git repo locally with:

```
mkdir enterprise
cd enterprise
git init
```

Created empty `enterprise` repositories/projects in each of the SCMs. (TODO: Script repo creation with APIs)

Then ran this snippet to create git remotes for each of the SCMs:

```
for scm in codeberg.org gitlab.com github.com; do git remote add "$scm" "git@${scm}:devopscoop/$(basename $PWD).git"; done; git remote -v;
```

To fetch code from all remotes use:

```
git pull --all
```

To push code to all remotes, add this to your `${HOME}/.gitconfig`:

```
[alias]
        pushall = !git remote | xargs -L1 git push --all
```

then run:

```
git pushall
```
