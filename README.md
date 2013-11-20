gerrit-kata
===========

Workshop about gerrit

## Introduction
http://gerrit-documentation.googlecode.com/svn/Documentation/2.3/intro-quick.html

## Workflow
http://source.android.com/source/life-of-a-patch.html

## Quickstart

* Clone git repository: `repo url`
* Install git commit-id hook to your local repo `scp -p -P 29418 review.example.com:hooks/commit-msg .git/hooks/`

## Working with changes and patchsets

```bash
$ git commit --amend
$ git push origin HEAD:refs/for/master
```

## Reviewing and submitting changes

## Resolving conflicts

## Gerrit magic
