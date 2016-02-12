# A `git` Tutorial for Busy Developers

###### Jonathan Cone, 2016 

##### Setup
1. [Download and install the git tools](https://git-scm.com/downloads)
2. Open up a terminal (Linux) or Git Bash (Windows) and configure `git`

  ```
  git config --global user.name "John Doe"
  git config --global user.email johndoe@example.com
  git config --global --add alias.lol "log --graph --decorate --pretty=oneline --abbrev-commit --all"
  ```
  
##### Making Changes
1. Create a new project and let git know we want to version control it
  
  ````    
  cd ~
  git init git-busy
  cd git-busy
  ````
1. Create a README file for our project

  ```
  echo The git-busy README file > README.md
  ```
1. View the status of the repository
  
  ```
  git status
  ```

1. Add the README.md file to the "stage", sometimes called the "index" to make it tracked

  ```
  git add README.md
  ```
1. View the status, notice that the file has been "staged" for commit
  
  ```
  git status
  ```
1. Commit the change to your repository
  
  ```
  git commit -m "Adding README file"
  ```
1. See the details of your recent commits
  
  ```    
  git log -5    # log supports many arguments, i.e. the last 5 commits
  git lol       # our aliased log format that we configured
  ```
1. Notice the hash code from the commit log, thats the universal commit ID for that change
1. Make a change to your file, restage it and commit in one step

  ```
  echo More coming soon... >> README.md
  git commit -a -m "Updating README"
  ```
1. Now view the log again and observe your new commit at the top

  ```
  git log
  ```
1. Compare the latest commit with the previous one
  
  ```
  git diff HEAD^
  ```
1. Check out the previous commit
  
  ```
  git checkout HEAD^
  cat README.md
  ```
1. Now switch back to the latest commit
  
  ```
  git checkout master
  cat README.md
  ```
  
##### Sharing Changes  
1. Everything up until this point has been local, but now we want to push it to a remote server -- we'll just use a different directory to emulate the remote server, but this would normally be a URL
  
  ```
  git init --bare ~/remoterepo.git
  git remote add origin ~/remoterepo.git
  ```
1. Now you can view the configured remote repository
  
  ```
  git remote -v
  ```
1. Let's push our changes to the remote

  ```
  git push -u origin master
  ```
1. Let's clone the repository from the remote URL like a teammate would

  ```
  git clone ~/remoterepo.git ~/another-busy
  cd ~/another-busy
  git log
  cd ~/git-busy
  rm -rf ~/another-busy
  ```
##### Branching
1. Branches are very light in git and extremely powerful, let's create one for a new feature we're adding

  ```
  git checkout -b feature_x
  ```
1. Now let's take a look at our branches

  ```
  git branch -avv
  ```
Notice that `feature_x` has an asterisk next to it, this is our current branch.  You'll also see the `master` branch which has `[origin/master]` next to the commit message.  This means that the `master` branch is tracking to the `master` branch on the remote server that we named `origin`. We're not tracking `feature_x` remotely.
1. Let's add our feature, an html version of the README file

  ```
  cp README.md README.html
  git add .
  git commit -m "Adding the README in html format"
  ```
1. We decided to make some more changes to the html README

  ```
  echo "<h1>Welcome</h1>" >> README.html
  git commit -am "Adding welcome message"
  git lol
  ```
1. At this point, we're finished with our feature. We want to make sure we're up to date with the latest from the remote repository so let's make sure our local `master` is up to date

  ```
  git checkout master
  git fetch origin
  git merge origin/master
  ```
1. Now we'll merge the local master into our `feature_x` branch before we merge `feature_x` into `master` so that we can fix any conflicts in our `feature_x` branch, not in `master`

  ```
  git checkout feature_x
  git merge master
  ```
1. Our `feature_x` branch is now up to date with the latest from `master` so we'll merge it and delete it

   ```
   git checkout master
   git merge feature_x
   git branch -d feature_x
   ```
1. Let's review the log

  ```
  git lol
  ```
The feature_x branch is gone and the master branch contains the commit message from our feature branch
1. Let's push our changes upstream to the remote repository so others can pull them down

  ```
  git push -u origin master
  ```
