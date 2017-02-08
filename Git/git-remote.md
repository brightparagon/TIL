#When unable to fetch from or push to remote repository we want?

It happens sometimes we need to push changes to a new remote repository. If we stage, commit and push right away, git will emit an error saying like **“fatal: remote origin already exists”** because the existing(currently used) remote url is conflicting with the one we want to push to.

###So how to solve it?

There are useful git commands for all cases related to remote repository url.

1. ``` git remote -v``` shows the current url
2. ``` git remote show ``` shows the added remote
3. ``` git remote show <name> ``` shows the url of *name* remote
4. ``` git remote add <name> ``` adds a new remote
5. ``` git remote set-url <name> <newurl> ``` changes the url of *name* remote to *newurl*

In this case we need to change the remote url to the one we want using ``` git remote set-url origin <newurl> ```

###Reference
http://stackoverflow.com/questions/10904339/github-fatal-remote-origin-already-exists

https://git-scm.com/docs/git-remote
