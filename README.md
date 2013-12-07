gerrit-kata
===========

Workshop about gerrit

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

### Exercise 1. Ammending commits
1. Edit `attendees` file and put you name with an error.
2. Commit and Push to refs/for/master
3. Find your change on gerrit
4. Ask person from your pair to review. During the review he/she should post some comments.
5. Fix the error and --amend your commit: `$ git commit --amend`
6. Push commit to refs/for/master again: `$ git push origin HEAD:refs/for/master`
7. Ask for review

### Exercise 2. Squashing commits
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

5. Push commit to/refs/for/master
6. Ask for review

### Exercise 3. Resolving conflicts
1. Edit `conflicts` file and add some random line
2. commit and push to refs/for/master
3. `git reset --soft HEAD~1` to move your head to the previous state
4. Change the same line in `conflicts` and push it to `origin HEAD:refs/for/master`
5. You should have two changes on gerrit affecting the same file
6. Review one of them and submit
7. Try to submit conflicting change. You should get an error.
8. `git fetch` and `git rebase`
9. Resolve conflict and `git rebase --continue`
10. `git push origin HEAD:refs/for/master`
11. Review the change on gerrit and submit. Now it should be merged succesfully.

## Gerrit and Jenkins
### Jenkins URL
* jenkins: http://54.194.88.176:8080/

### Code Verification
* automated tests
* static analysis

### Exercise 4. Commiting broken build
1. Create new mocha failing test in `test` folder. It can be as simple as this:

```javascript
var expect = require('chai').expect;

describe("Add numbers" , function(){
    it("dwa plus dwa powinno dac Siedemset", function(){
        expect(2+2).to.equal(700);
    });
});
```

2. Commit and push test to `refs/for/master`
3. When you go to gerrit, you should be able to see that the code was verified by Jenkins and rejected.
4. Fix the test which doesn't make sense.
5. `commit --amend` and push code again.
6. Now you should see that the tests are passing in jenkins and change is verified.

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
