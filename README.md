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

### Ammending commits
```bash
$ git commit --amend
$ git push origin HEAD:refs/for/master
```

### Squashing commits
`git rebase -i HEAD~3`

```
pick f392171 Added new feature X
pick ba9dd9a Added new elements to page design
pick df71a27 Updated CSS for new elements
```

```
pick f392171 Added new feature X
squash ba9dd9a Added new elements to page design
squash df71a27 Updated CSS for new elements
```

## Reviewing and submitting changes

## Resolving conflicts

## Gerrit tips
### Configuration
* Adding verified label: https://gerrit-review.googlesource.com/Documentation/config-labels.html

`git pull ssh://rscheibinger@54.194.88.176:29418/All-Projects HEAD:refs/meta/config`
`git push ssh://rscheibinger@54.194.88.176:29418/All-Projects HEAD:refs/meta/config`
`ssh -p 29418 jenkins@54.194.88.176 gerrit review 2,8 --verified=-1 --code-review 0`

## Additional resource:
* setting up gerrit with jenkins: http://dachary.org/?p=1716
* https://code.google.com/p/gerrit/
