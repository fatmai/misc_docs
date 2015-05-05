### A selection of commands

**Check git commit status**

~~~ 
git status
~~~ 

**See all the commits**

~~~ 
git log
~~~ 

**Which files are tracked**

~~~ 
git ls-files
~~~ 

**Remove files from repo**

~~~ 
git rm file.txt

git commit -m "remove file.txt"
~~~ 

**Move files within or from repo**

~~~ 
git mv file.txt ~

git commit -m "file.txt moved to home-dir"
~~~ 

**Stash and drop changes when conflict between versions**

~~~
git stash save --keep-index
~~~

### A general workflow

1. Fork a repository (e.g. *music.features* from the *gallantlab* organization into *fatmai/music.features*)

2. Create a new branch for each logically connected work unit you will change

	~~~
	git checkout -b <branch-name>
	~~~

3. Do whatever changes you want to make in this branch. Make several commits.

4. Push all the changes to your github repository e.g. *fatmai* 

	~~~
	git push fatmai <branch-name>
	~~~

**CAUTION**

<Everything that can go wrong should come here.>



### DEALING WITH Changing the Repositories owner

Scenario:

I changed the github repository "music.features" under the user *fatmai* to be under the organisation *gallantlab*. Subsequently on github, I forked the *gallantlab/music.features* repository to *fatmai/music.features*. These changes now need to be made effective in the local machines that already had a clone from the *fatmai/music.features* repository.

* First check what remote repositories you have access to

	~~~ 
	$ git remote -v
	
	origin	https://github.com/fatmai/music.features.git (fetch)
	origin	https://github.com/fatmai/music.features.git (push)
	~~~ 
	
* Remove this local repository that is pointing to *nirvana*

	~~~ 
	$ git remote rm origin 
	~~~ 

* Add the new repository under *gallantlab* organization as the *origin* remote repository

	~~~ 
	$ git remote add origin https://github.com/gallantlab/music.features.git
	~~~ 
	
* Add the new repository under *fatmai* organization as the *fatmai* remote repository

	~~~ 
	$ git remote add fatmai https://github.com/fatmai/music.features.git
	~~~ 
	
* Check the remote repositories again

	~~~ 
	$ git remote -v

	fatmai	https://github.com/fatmai/music.features.git (fetch)
	fatmai	https://github.com/fatmai/music.features.git (push)
	origin	https://github.com/gallantlab/music.features.git (fetch)
	origin	https://github.com/gallantlab/music.features.git (push)
	~~~ 
	
* One last complain: Pull request from the master branch will result in the following

	~~~ 
	$ git pull
	
	From https://github.com/gallantlab/music.features
 	* [new branch]      master     -> origin/master
 	* [new branch]      test_fixes -> origin/test_fixes
	There is no tracking information for the current branch.
	Please specify which branch you want to merge with.
	See git-pull(1) for details

    git pull <remote> <branch>

	If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream master <remote>/<branch>
	~~~ 
	
* Tell your local git which repositories the branches belong to

	~~~ 
	$ git branch --set-upstream master origin/master
	~~~ 

* this should work now:

 	~~~ 
	$ git pull
	~~~ 

### A solution to "Your branch is X commits ahead"

Scenario: You made changes in your local master copy but did not push them.
(You can compare the git logs between your local and remote branch to see what 
has not been commited.) There are different solutions:

- If you want to keep these commits, you can push your local changes to the
  remote repository:

	~~~ 
    $ git push origin assuming origin is your remote
	~~~ 

- If you don't want to keep these changes then remove them or reset your local master
to the state on remote by doing:

	~~~ 
    $ git reset --hard origin/master
	~~~ 

How to avoid this message in the future:

- In general your remote master repository should be the clean repository and
  the local master repository a copy of the remote one.


### DEALING WITH SWC Pull requests

* Create your own change-whatever branch

	~~~ 
	git checkot -b change-whatever
	~~~ 

* Check what remote branches you have access

	~~~ 
	git remote -v
	~~~ 

* Add remote upstream swcarpentery/shell-novice branch

	~~~ 
	git remote add upstream https://github.com/wcarpentry/shell-novice.git
	~~~ 

* Now you should be able to see https://github.com/swcarpentry/shell-novice.git as upstream when you do 
	
	~~~ 
	git remote -v
	~~~

* Pull changes from swcarpentery/shell-novice, which is your upstream. You want to be up-to-date before moving forward.
	
	~~~ 
	git pull upstream gh-pages
	~~~ 
	
* Make your changes *

	~~~ 
	vi 06-find.md
	~~~ 

* Commit your changes. Commit them line by line and push after each commit.

	~~~ 
	git commit -am "Comment from @r-gaia-cs. Adds backticks to line 116"
	~~~ 

* Push to origin branch gh-pages
* 
	~~~ 
	git push origin gh-pages
	~~~ 
	
 	==> Now when you go on github the open issue will be gone. So if there are many comments to one issue, first clean everything. make commits to each separately and then when you have finalized push it to the origin branch. 

