gerrit-kata
===========

Workshop about gerrit

## Introduction
http://gerrit-documentation.googlecode.com/svn/Documentation/2.3/intro-quick.html

## Workflow
http://source.android.com/source/life-of-a-patch.html

## Quickstart
###URLs
* gerrit: http://54.194.88.176:8081/
* jenkins: http://54.194.88.176:8080/

### Become the user
* Click become the user

#### Authentication methods
* SSH keypair
  * Add ssh public key/generate password for http authen
* HTTP
  * set username and generate password

####Creating project
ssh -p 29418 admin@54.194.88.176 gerrit create-project --name gerrit-kata

* Clone git repository: `git clone ssh://your_username@54.194.88.176:29418/gerrit-kata` or http://54.194.88.176:8081/#/admin/projects/gerrit-kata
* Try to commit and push anything
* Install git commit-id hook to your local repo to fix the error `scp -p -P 29418 review.example.com:hooks/commit-msg .git/hooks/`

## Working with changes and patchsets

```bash
$ git commit --amend
$ git push origin HEAD:refs/for/master
```

## Reviewing and submitting changes

## Resolving conflicts

## Gerrit magic
