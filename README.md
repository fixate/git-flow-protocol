# Git Flow Protocol

Git Flow has a few nuances in workflow that can be difficult to grasp or understand.

Most of the workflow can be understood by reading through the [Git Flow Cheatsheet](http://danielkummer.github.io/git-flow-cheatsheet/).

## Setup

At Fixate we use the default setup for git flow on all projects:

```shell
$ git flow init -d
```

Work is branched off of develop using feature branches.

Production ready code is available in master. If something is not production ready, it should not be in master.

Hotfixes are for quick fixes required on production code. Hotfixes are automatically branched off of master, and merged into both master and develop.

## Working With Hotfixes

### 1. Checkout And Pull Master

Before making a hotfix, make sure to be on the tip of master, as master is where hotfixes are branched from:

```shell
$ git checkout master
$ git pull
//=> get tip of master
```

### 2. Check Existing Tags

Once you are on the tip of master, check for the latest tag, and create a hotfix as an increment of that tag:

```shell
$ git tags
1.0.1
1.0.2
1.0.3

$ git flow hotfix start 1.0.4
//=> creates new branch hotfix/1.0.4
```

### 3. Working And Finishing Hotfix

Make the changes, test that they are working, and then finish your hotfix:

```shell
$ git flow hotfix finish 1.0.4
//=> changes merged into master and develop
//=> new tag 1.0.4 created
//=> hotfix branch deleted
//=> checkout develop
```

### 4. Pushing Changes And Tags

Push your changes and tag up to the server, so that everyone knows the subsequent tag to create for further hotfixes:

```shell
$ git push --all && git push --tags
//=> push updates on master and develop to origin
//=> push new tag to origin
```
