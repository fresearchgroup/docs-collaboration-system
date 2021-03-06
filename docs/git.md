---
id: git
title: Git branching models and commands
sidebar_label: Git Models and Commands
---

Git is a version control system for tracking changes in computer files and coordinating work on those files


## Initializing a new repository -  

```
$ git init
```

## Add files to staging area
```
  $ git add <filename or .>
```

## Commit the files
```
$ git commit -m “message”
```

## Cloning an Existing Repository
```
$ git clone    https://github.com/fresearchgroup/Collaboration-System.git
```

## Checking the Status of Your Files in a repository
```
	$ git status
```

Ignoring Files to be added in a staging area while adding or committing . Create a file and list all the file and directory patterns which will ignore all the file that will match the pattern
```
$ touch .gitignore
```

## To know exactly what has changed, just which files were changed — use
```
	$ git diff
```

## To show all your remotes
```
	$ git remote -v
```

## Adding Remote Repositories - git clone command implicitly adds the origin remote for you. Here’s how to add a new remote explicitly.
```
$ git remote add abhi https://github.com/abhisgithub/Collaboration-System.git
```
## To pull the changes from the remote repo that you clone from use-
```
	$ git pull   
```

Running git pull generally fetches data from the server you originally cloned from and automatically tries to merge it into the code you’re currently working on.

Fetch all the information from another remote - if you want to fetch all the information that abhisgithub has but that you don’t yet have in your repository, you can run -

```
	$ git fetch abhi
```
Note: -It’s important to note that the git fetch command only downloads
the data to your local repository — it doesn’t automatically merge it with any of your work or modify what you’re currently working on. You have to merge it manually into your work when you’re ready.

## Pushing to Your Remotes
```
	$ git push origin master
```

## Inspecting a Remote -- If you want to see more information about a particular remote, you can use
```
	$ git remote show origin
```

## Renaming Remotes
```
	$ git remote rename abhi ab
```

## Removing Remotes
```
	$ git remote remove ab
```

## Tagging
Listing Your Tags
```
	$ git tag
```

## Creating Tags -

	Git supports two types of tags: lightweight and annotated.

A lightweight tag is very much like a branch that doesn’t change —it’s just a pointer to a specific Commit. To create a light weight tag
```
$ git tag v1.4-lw
```

Annotated tags, however, are stored as full objects in the Git database. Creating an annotated tag in Git is simple. The easiest way is to specify -a when you run the tag command. We shall use this method for tagging:
```
$ git tag -a v1.4 -m "my version 1.4"
```

Tagging Later - if you forgot to tag the project at v1.2, which was at the “particlar” commit. You can add it after the fact. To tag that commit, you specify the commit checksum (9fceb02) at the end of the command:
```
	$ git tag -a v1.2 9fceb02
```

Sharing Tags - the git push command doesn’t transfer tags to remote servers.
	To explicitly push tags to a shared server after you have created them.
```
	$ git push origin <tagname>
```
	To transfer all of your tags to the remote server at once
```
  $ git push origin --tags
```

## Git Branching

Creating a New Branch
```
	$ git branch testing
```
	This creates a new pointer to the same commit you’re currently on.

Switching Branches
```
	$ git checkout testing
```
	checkout command is use to switch branches.

To print out the history of your commits, showing where your branch pointers are and how your history has diverged.
```
  $ git log --oneline --decorate --graph --all
```

To merge two branches example -- merge the hotfix branch back into your master branch to deploy to production. You do this with merge command:
```
	$ git checkout master
	$ git merge hotfix
```

To list the current branches -
```
	$ git branch -v
```

## Branching Models -

Other than master and develop branches, there are some short live branches.These branches always have a limited lifetime, since they will be removed eventually.
They are -
- Feature branches
- Release branches
- Hotfix branches

## Feature branches -
 To create new feature branch, branch off from the develop branch.
 ```
		$ git checkout -b myfeature develop
```

After finishing a feature,  merged into the develop branch
```
	$ git checkout develop
	$ git merge --no-ff myfeature
	$ git branch -d myfeature
  $ git push origin develop
```

## Release branches -
 To create new release branches are created from the develop branch.(when the state of develop is ready for the “next release”)
 ```
		$ git checkout -b release-1.2 develop
 ```
After finishing a release branch --
```
	$ git checkout master
  $ git merge --no-ff release-1.2
  $ git tag -a 1.2
```
 The changes that are made in the release branch, are also  need to merge back into develop, branch.
 ```
	$ git checkout develop
	$ git merge --no-ff release-1.2
	$ git branch -d release-1.2
```
## Hotfix branches -
Hotfix branches are created from the master branch
eg:  tag 1.2 is on production release running live and causing troubles due to a severe bug. And develop is still unstable then , create a Hotfix branch and start fixing the problem:
```
$ git checkout -b hotfix-1.2.1 master
```
Make the changes needed in hotfix branch
```
$ git commit -m "Fixed severe production problem"
```
The bugfix needs to be merged back into master,
```
$ git checkout master
$ git merge --no-ff hotfix-1.2.1
$ git tag -a 1.2.1
```
The bugfix needs to be merged back into develop,
```
$ git checkout develop
$ git merge --no-ff hotfix-1.2.1				
$ git branch -d hotfix-1.2.1
```

## Workflow for Collaborators
This workflow should be followed by all collaborators of the project, i.e. existing staff and RAs.

Clone the repository and work in respective feature branches.
Merge it to develop branch
Make pull request to master branch


## Workflow for a new comer
The following workflow should be followed by a new comer i.e.  interns or a new joinee.

Fork the repository
Work on existing feature branch or create a feature branch of your own
Create a pull request for develop branch

## Working with forking Repositories
 TO sync the repository with origin repo use following command

```
$ git remote add upstream original_repo_url
$ git fetch upstream
$ git checkout master
$ git rebase upstream/master
$ git push origin master
```

For advance reading , download Pro Git

https://github.com/progit/progit2/releases/download/2.1.38/progit.pdf
