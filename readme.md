# NOTES
_____


## Add a repo as a submodule in git

To add a new submodule you use the `git submodule add` command with the absolute or relative URL of the project you would like to start tracking. In this example, we’ll add a library called “DbConnector”.
```  
git submodule add https://github.com/chaconinc/DbConnector
```

## Cloning a repo that contains submodule

When you clone such a project, by default you get the directories that contain submodules, but none of the files within them yet:

```
git clone https://github.com/chaconinc/MainProject
```

 To also initialize, fetch and checkout any nested submodules, you can use the foolproof 
 ```
 git submodule update --init --recursive
 ```

## Working on a Project with Submodules

### Pulling in Upstream Changes from the Submodule Remote

If you want to check for new work in a submodule, you can go into the directory and run `git fetch` and `git merge` the upstream branch to update the local code. 

To make the latest checkout the default version for the parent repo, commit the parent repo after going to the parent base dir. and then push the changes.

### Make changes in a git submodule

#### NOTE: Before doing any work in the submodule checkout to a branch inside the submodule, because by default there wont be any branch to keep track the submodule

#### A submodule is its own repo/work-area, with its own .git directory. 

So, first commit/push your submodule's changes:
```
$ cd path/to/submodule
$ git add <stuff>
$ git commit -m "comment"
$ git push
```
Then, update your main project to track the updated version of the submodule:
```
$ cd /main/project
$ git add path/to/submodule
$ git commit -m "updated my submodule"
$ git push
```

## Removing a file from all previous commits and making it reflect in the remote

syntax is `git filter-branch --tree-filter <command> ...`

`git filter-branch --tree-filter 'rm -f Resources\Video\%font%.ttf' -- --all`


Explanation about the command:

`< command >`: Specify any shell command.

`--tree-filter`: Git will check each commit out into working directory, run your command, and re-commit.

`--all`: Filter all commits in all branches.


**Example:**
''' sh
git filter-branch --tree-filter 'rm -f <file-name>' -- --all
git push --force origin <branch-name>
'''

## Stop git from tracking a previously tracked file

Your .gitignore is working, but it **still tracks the files because they were already in the index.**

To stop this you have to do : `git rm -r --cached <location>`