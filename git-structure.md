#Git structure
This is a guide for using a particular git branching model when working on a
bigger development project where more developers are involved. This model was
introduced by *Vincent Driessen* in his 
[article](http://nvie.com/posts/a-successful-git-branching-model/)
where you can read about it more indepth with all the explanations and whatnots.

##Overview
The following picture illustartes the big picture of the whole branching model
used for big development projects. You can see different branches living side by
side more or less over the lifetime of the whole project.

![Git structure](assets/git-structure/git-structure.png)

Let's dive into the description of all the different branches so we will know
what they are used for.

##Main branches

###master
This is the main and default branch created by GIT itself when initializing any
GIT based repository. In this model however, the `master` branch is a production
ready code which has to be stable and ready for deployment at any given time.
Basically it is the same exact code which is used on production server and on
which the application is running for the whole public.

###develop
This branch is considered as the main development branch, which represents the
latest delivered changes for the release. When the development changes reaches
a stable point, this branch is ready to be marged back into `master` branch.
There are several ways how to merge it though, so stay tuned.

##Supporting branches

###feature
This branch is used for more convinient parallel development of changes within
a larger group of developers. Every developer can work on his particular part
of the code and once the feature is ready, it can be merged back into the 
'develop' branch. The 'feature' branches usually exists on developer local
repositories and not on the central (origin) repository. There may be some
exception to this rule, if more than one developer is working on some particular
feature or if the feature is really complex.

The `feature` branch is always branched of the `develop` branch and must be
always merged back to `develop` branch after the feature is developed.

To create new `feature` branch
```
$ git checkout -b feature-name develop
```

To merge back to `develop` branch once the feature development is complete:
```
$ git checkout develop
$ git pull
$ git merge --no-ff feature-name
$ git branch -d feature-name
$ git push origin develop
```

###release
We have already spoken about one way of merging `develop` into `master` branch
which may be the case of some middle sized project, but in bigger projects we
usually use the supporting `release` branch. The benefit of such branch is that
it allows for preparation of production realease like last-minute bugfixing,
metadata preparation, configuration modification, while the `develop` branch is 
ready to receive new modifications for the next upcoming realease.

The `release` branch must be branched of `develop` branch at a time, when all
the features targeted for next release are developed and merged into `develop`
branch. The `release` branch must merge back to `master` and `develop` branches.
(The additional merge back to `develop` is due to the possible cahnges,
bugfixes, metadata and configuration modifications in `release` branch). It is 
also considered best-practice to create new tag on `master` branch once the
`release` branch is merged into it.

To create new `release` branch:
```
$ git checkout -b release-1.1 develop
# modify metadata for versioning, modify configuration for production env.
$ git commit -m "Bumped verioning, configured for production"
# possible further bugfixes
```

To merge back to `master` and `develop` branches and create a new tag:
```
$ git checkout master
$ git pull
$ git merge --no-ff release-1.1
$ git tag -a 1.1
$ git push origin master
$ git chcekout develop
$ git pull
$ git merge --no-ff release-1.1
$ git branch -d release-1.1
$ git push origin develop
```

