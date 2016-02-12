Git Tutorial README
---------------------------

# Install and configure Git
    git config --global user.name "John Doe"
    git config --global user.email johndoe@example.com
    git config --global --add alias.lol "log --graph --decorate --pretty=oneline --abbrev-commit --all"

# Create a new repository
    
    git init portfolio-manager

# Create a README file

    echo A fun README file > README.md

# View the status, notice that the file in untracked, version control isn't managing this file

    git status

# Add the README.md file to the index

    git add README.md

# View the status, notice that the file has been "staged" for commit

    git status

# Commit the change to your repository

    git commit -m "Adding README file"

# See the details of your recent commits
    
    git log -5    # log supports many arguments, i.e. the last 5 commits
    git lol       # our aliased log format that we configured

# Make a change to your file, restage it and commit

    echo Coming soon... >> README.md
    git commit -a -m "Updating README"



