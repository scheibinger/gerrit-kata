gerrit-kata
===========

Workshop about gerrit

## Introduction
http://gerrit-documentation.googlecode.com/svn/Documentation/2.3/intro-quick.html

## Workflow
* http://source.android.com/source/life-of-a-patch.html
* Diagram: http://source.android.com/images/workflow-0.png

## Quickstart
###URLs
* gerrit: http://54.194.88.176:8081/

### Become the user
* Click become the user

#### Authentication methods
* SSH keypair
  * Add ssh public key/generate password for http authen
* HTTP
  * set username and generate password

### Clone gerrit-kata git project

ssh -p 29418 admin@54.194.88.176 gerrit create-project --name gerrit-kata

* Clone git repository: `git clone ssh://your_username@54.194.88.176:29418/gerrit-kata` or http://54.194.88.176:8081/#/admin/projects/gerrit-kata
* Try to commit and push anything
* Install git commit-id hook to your local repo to fix the error `scp -p -P 29418 review.example.com:hooks/commit-msg .git/hooks/`

## Working with changes and patchsets
In this exercise you will learn how to push your changes to gerrit and how the review functionality works.

### Ammending commits
1. Edit `attendees` file and put you name with an error.
2. Commit and Push to refs/for/master
3. Find your change on gerrit
4. Ask person from your pair to review
5. Fix the error and --amend your commit: `$ git commit --amend`
6. Push commit to refs/for/master again: `$ git push origin HEAD:refs/for/master`
7. Ask for review

### Squashing commits
1. Create a file with your name, add some bad content and push it to refs/for/master
2. Ask for review. The result should be negative.
3. Make a few commits to fix the bad content.
4. Squash commits with intermediate steps to fix the bad content:
`git rebase -i HEAD~3`

After entering the command you will see following commit message:

```
pick f392171 Added new feature X
pick ba9dd9a Added new elements to page design
pick df71a27 Updated CSS for new elements
```

In order to squash the last commits change `pick` into `squash` in front of the commit hash:

```
pick f392171 Added new feature X
squash ba9dd9a Added new elements to page design
squash df71a27 Updated CSS for new elements
```

5. Push the commit to/refs/for/master
6. Ask for review

## Resolving conflicts

## Gerrit and Jenkins
### Jenkins URL
* jenkins: http://54.194.88.176:8080/

### Code Verification
* automated tests
* static analysis

## Gerrit tips
### Creating project from cmd line:
`ssh -p 29418 admin@54.194.88.176 gerrit create-project --name gerrit-kata`
### Configuration
* Adding verified label: https://gerrit-review.googlesource.com/Documentation/config-labels.html

`git pull ssh://rscheibinger@54.194.88.176:29418/All-Projects HEAD:refs/meta/config`
`git push ssh://rscheibinger@54.194.88.176:29418/All-Projects HEAD:refs/meta/config`
`ssh -p 29418 jenkins@54.194.88.176 gerrit review 2,8 --verified=-1 --code-review 0`

## Additional resource:
* setting up gerrit with jenkins: http://dachary.org/?p=1716
* https://code.google.com/p/gerrit/
