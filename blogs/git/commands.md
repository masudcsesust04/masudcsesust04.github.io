# GIT essential commands

Clone remote repository
```
$ git clone [repository_url]
```

Initialize an existing project
```
$ cd /home/path/project_name/
$ git init
$ git add .
$ git commit -m "first commit"
$ git remote add origin [repository_url]
$ git push -u origin master
```

Add remote[github, bitbucket or gitlab etc.] repository
```
$ cd /home/path/project_name/
$ git remote add origin [repository_url]
$ git push -u origin master
```

Add a new remote(except ```origin``` for example ```dev```)
```
$ git remote add [origin_name] [remote_repository_url] 
```

Change/update remote repository URL
```
$ git remote set-url origin repository_url
$ git remote set-url --push origin repo_url
```

Check remote origin
```
$ git remote show origin
or 
$ git remote -v
```

Check list of local branches
```
$ git branch
```

Check list of remote branches
```
$ git branch -r
```

Check list of local and remote branches
```
$ git branch -a
```

Checkout a local branch from branch list
```
$ git checkout [branch_name] 
```

Create new branch from current branch
```
$ git checkout -b [branch_name]
```

Create and checkout new branch from remote branch
```
$ git checkout -b [branch_name] [remote_name]/[branch_name]
```

Push new branch to the remote repository
```
$ git push origin [branch_name]
```

Rename the current working branch
```
$ git branch -m [new_branch_name]
```

Rename a branch while pointed to a different branch
```
$ git branch -m [new_branch_name] [old_branch_name]
```

Push renamed branch to the remote repository
```
$ git push origin :[new_branch_name]
```

Push changes from your commit into your branch
```
$ git push [name_of_your_new_remote] [name_of_your_branch]
```

Delete a local branch 
```
$ git branch -d [branch_name]
```

Force delete of local branch
```
$ git branch -D [branch_name]
```

Delete the branch form remote(push deleted branch to remote repository)
```
$ git push origin :[branch_name]
```

Update remote branch list
```
$ git remote update origin --prune
```

Checkout a specific remote branch
```
$ git fetch
$ git checkout [branch_name]
```

Fetch all remote branches(it will also remove local branches which are remotely deleted)
```
$ git fetch -p
```

Checkout to a branch from remote branch list
```
$ git fetch origin
$ git checkout -b [branch_name] [origin/branch_name]
```

Untrack a file form git
```
$ git rm --cached [file_name_with_path]
```

Rollback to previous commit
```
git reset HEAD~1
```

Rebase a branch with current working branch
```
$git rebase [branch_name]
```

Merge a branch with current working branch
```
$ git merge [branch_name]
```

TODO: Add instructions to change/modify commit message

