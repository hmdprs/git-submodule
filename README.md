# git-submodules

Git allows you to include other Git repositories called **submodules** into a repository. This allows you to track changes in several repositories via a central one. Git allows you to commit, pull and push to these repositories independently. Submodules allow you to keep projects in separate repositories but still be able to reference them as folders in the working directory of other repositories.

## Creating Repositories with Submodules

If you add a submodule, you can control which **commit** should be used.

```bash
# adds a submodule to an existing Git repository
git submodule add [URL to Git repo]

# defines that the master branch should be tracked
git submodule add -b master [URL to Git repo]
```

```bash
# initialize submodule local configuration
git submodule init
```

## Working with Repositories that contain Submodules

```bash
# clone a repository including its submodules
git clone --recursive [URL to Git repo]
```

```bash
# load it’s submodules to a cloned repository
git submodule update --init --recursive
```

```bash
git diff --cached --submodule
```

```bash
# pull all changes in the repo including changes in the submodules
git pull --recurse-submodules
```

For executing a command on every submodule:

```bash
git submodule foreach --recursive 'git reset --hard'
```

## Updating the Commit You are Tracking

The following example shows how to update a submodule to its latest commit in its master branch.

```bash
# update submodule in the master branch
# skip this if you use --recurse-submodules and have the master branch checked out
cd [submodule directory]
git checkout master
git pull

# commit the change in main repo to use the latest commit in master of the submodule
cd ..
git add [submodule directory]
git commit -m "move submodule to latest commit in master"

# share your changes
git push
```

Another developer can get the update by pulling in the changes and running the `submodules` update command.

```bash
# another developer wants to get the changes
git pull

# this updates the submodule to the latest commit in master as set in the last example
git submodule update
```

## Delete a Submodule

Currently Git provides no standard interface to delete a submodule. To remove a submodule called `mymodule` you need to:

```bash
git submodule deinit -f mymodule
rm -rf .git/modules/mymodule
git rm -f mymodule
```

## Credit

- [Using submodules in Git - Tutorial](https://www.vogella.com/tutorials/GitSubmodules/article.html)
- [Git Tools - Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)
- [git-submodule](https://git-scm.com/docs/git-submodule)
