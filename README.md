Git Tutorial README
---------------------------

# Create a new repository
    
    git init portfolio-manager

# Create a README file

    echo README File > README.md

# View the status, notice that the file in untracked, version control isn't managing this file

    git status

# Add the README.md file to the index

    git add README.md

# View the status, notice that the file has been "staged" for commit

    git status

# Commit the change to your repository

    git commit -m "Adding README file"
