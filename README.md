A Git Tutorial for Busy Developers

Jonathan Cone, 2016 
--------------------------------------

# Install and configure Git
    git config --global user.name "John Doe"
    git config --global user.email johndoe@example.com
    git config --global --add alias.lol "log --graph --decorate --pretty=oneline --abbrev-commit --all"

# Create a new project and let git know we want to version control it
    
    git init busy-tutorial && cd busy-tutorial

# Create a README file for our project

    echo A busy README file > README.md

# View the status, notice that the file in "untracked", this is just git's way
  of saying its not managing this file

    git status

# Add the README.md file to the "stage", sometimes called the "index"

    git add README.md

# View the status, notice that the file has been "staged" for commit

    git status

# Commit the change to your repository

    git commit -m "Adding README file"

# See the details of your recent commits
    
    git log -5    # log supports many arguments, i.e. the last 5 commits
    git lol       # our aliased log format that we configured

# Notice the hash code, thats the universal commit ID for that change

# Make a change to your file, restage it and commit in one step

    echo More coming soon... >> README.md
    git commit -a -m "Updating README"

# Now view the log using lol and notice that there are two changes, your 
  initial commit and your update

# Compare the latest commit with the previous one

    git diff HEAD^

# Check out the previous commit

   git checkout HEAD^
   cat README.md

# Now switch back to the latest commit

  git checkout -b master
  cat README.md

# 
    git init --bare ../remoterepo

Branching
Merging
Remotes
Tags

