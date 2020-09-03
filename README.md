# Git commands cheat sheet



This cheat sheet provides some handy commands to get you started with Git / GitHub.

## See also
__[Git / Github intro course on youtube](https://www.youtube.com/watch?v=U8GBXvdmHT4)__


## Repositories

### Create a new repo

```bash
$ git init
```

### See repo status

```bash
$ git status 
```

### Activate credentials caching

On Linux, if git keeps asking for your credentials, ([source](https://help.github.com/articles/caching-your-github-password-in-git/#platform-linux)):

```bash
$ git config --global credential.helper cache
$ git config --global credential.helper 'cache --timeout=3600'
```





### Get an existing repo from remote

```bash
$ git clone <url>
```


## Gitignore

Get rid of the dreaded `.DS_Store` files using: [https://gist.github.com/lohenyumnam/2b127b9c3d1435dc12a33613c44e6308](https://gist.github.com/lohenyumnam/2b127b9c3d1435dc12a33613c44e6308)


## Branches

### Misc
List branches

```bash
// Local only
$ git branch

// Local and remote
$ git branch -a
```

Switch from current local branch to another local branch

```bash
$ git checkout <branch-name>
```


Refresh branch from remote

```bash
// Checkout the branch first
$ git checkout <branch-name>

$ git pull
```



### Creating branches

Create a new local branch

```bash
$ git branch <branch-name> 
```


Create remote branch

Push content of a new local branch on the remote repo:

```bash
$ git push -u origin <branch-name>
```



Get a branch from remote

```bash
$ git checkout -b <branch-name> origin/<branch-name>
```



### Committing work to a branch

Specifying a new file needs to be tracked by the repo

```bash
$ git add <file-name>
```


Committing work to the local repo

```bash
$ git commit -m '<message>'
```

Updating the remote repo

```bash
$ git push
```




### Merging branches

Merge `branchB` into `branchA`

```bash
$ git checkout branchA
$ git merge branchB
```



Merge `branchB` into `branchA` and resolve all conflicts using the artifacts from `branchA` 

```bash
$ git checkout branchA
$ git merge -s ours branchB
```


Merge `branchB` into `branchA` and resolve all conflicts using the artifacts from `branchB` 

```bash
$ git checkout branchA
$ git merge -X theirs branchB
```

Rollback a merge (useful if you have conflicts).

```bash
$ git reset --merge
```




### Deleting branches

Delete local branch

```bash
$ git branch -D <new-branch>
```


Delete a branch from remote

```bash
$ git push origin --delete <new-branch>
```











## Tags

Add a tag ```<tagname>``` (for a release for example):

```bash
// Add to the local repo
$ git tag <tagname>

// Add to the remote repo
$ git push origin <tagname>
```

Retrieve tags from remote:

```bash
$ git fetch --tags
```

List local tags:

```bash
$ git tag
```

Remove a tag ```<tagname>```:

```bash
// Delete locally
$ git tag --delete <tagname>

// Delete on remote
$ git push origin :refs/tags/<tagname>
```














## Use case: locally add branch, do work and merge back into another branch



Clone the remote repo on your local workstation

```bash
$ git clone <url>
```

Create a new branch named ```<new-branch>```, (or get an existing branch from remote instead, see relevant command earlier in the cheat sheet).

```bash
$ git branch <new-branch> 
```

Toggle to the branch ```<new-branch>```

```bash
$ git checkout <new-branch>
```

(Do some work)

Add the changes

```bash
$ git add .
```

Commit the changes

```bash
$ git commit -m "Commit message here"
```

Merge branch ```<new-branch>``` into ```<old-branch>```. For a merge into `master`, you will usually submit a pull request to the repo owner instead. The repo owner will review the changes and do the merge for you.

```bash
$ git checkout <old-branch>
$ git merge <new-branch>
```

Push to the remote repo

```bash
$ git push origin <old-branch>
```

