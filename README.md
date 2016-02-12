# A `git` Tutorial for Busy Developers

###### Jonathan Cone, 2016 

1. [Download and install git](https://git-scm.com/downloads)
2. Open up a terminal (Linux) or Git Bash (Windows) and configure git 

  ```
  git config --global user.name "John Doe"
  git config --global user.email johndoe@example.com
  git config --global --add alias.lol "log --graph --decorate --pretty=oneline --abbrev-commit --all"
  ```
1. Create a new project and let git know we want to version control it
  
  ````    
  cd ~
  git init git-busy
  cd git-busy
  ````
1. Create a README file for our project

  ```
  echo A busy README file > README.md
  ```
1. View the status, notice that the file in "untracked", this is just git's way of saying its not managing this file
  
  ```
  git status
  ```
1. Add the README.md file to the "stage", sometimes called the "index"

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
1. Notice the hash code, thats the universal commit ID for that change
1. Make a change to your file, restage it and commit in one step

  ```
  echo More coming soon... >> README.md
  git commit -a -m "Updating README"
  ```
1. Now view the log using lol and notice that there are two changes, your initial commit and your update
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
  git checkout -b master
  cat README.md
  ```
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
  ```
1. Now we switch back to our original workspace and to learn about branching

  ```
  cd ~/git-busy
  ```
1. Branches are very light in git and extremely powerful, let's create one for a new html tutorial feature we're adding

  ```
  git checkout -b html_tutorial
  ```
1. Now let's take a look at our branches

  ```
  git branch -avv
  ```
1. Notice that html_tutorial has an asterisk next to it, this is our current branch
