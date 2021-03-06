# A `git` Tutorial for Busy Developers

###### Jonathan Cone, 2016 

##### Setup
1. [Download and install the git tools](https://git-scm.com/downloads).
2. Open up a terminal (Linux) or Git Bash (Windows) and configure `git`:

  ```shell
  $ git config --global user.name "John Doe"
  $ git config --global user.email "x@example.com"
  $ git config --global --add alias.lol "log --graph --decorate --pretty=oneline --abbrev-commit --all"
  ```
  
##### Creating a Repository
1. Create a new project and let `git` know we want to version control it:
  
  ````shell    
  $ cd ~
  $ git init git-busy
  Initialized empty Git repository in ~/git-busy/.git/
  
  $ cd git-busy
  ````

##### Making Changes
1. Create a markdown-style README file for our project:

  ```shell
  $ echo The git-busy README file > README.md
  ```
1. View the status of the repository:
  
  ```shell
  $ git status
  On branch master
  
  Initial commit
  
  Untracked files:
    (use "git add <file>..." to include in what will be committed)
  
          README.md
  
  nothing added to commit but untracked files present (use "git add" to track)
  ```

1. Add the README.md file to the "stage", sometimes called the "index" to make it tracked:

  ```shell
  $ git add README.md
  ```
1. View the status, notice that the file has been "staged" for commit:
  
  ```shell
  $ git status
  On branch master
  
  Initial commit
  
  Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
  
          new file:   README.md
  ```
1. Commit the change to your repository:
  
  ```shell
  $ git commit -m "Adding README file"
  [master (root-commit) e3ede2c] Adding README file
   1 file changed, 1 insertion(+)
   create mode 100644 README.md
  ```
1. See the details of your recent commits:
  
  ```shell    
  $ git log
  commit e3ede2c3777b811feff99eee4a3a456a5030e340
  Author: John Doe <x@example.com>
  Date:   Fri Feb 12 14:42:31 2016 -0600
  
      Adding README file
  ```
Notice the hash code, thats the universal commit ID for that change.
1. Make a change to your file, restage it and commit in one step:

  ```shell
  $ echo More coming soon... >> README.md
  $ git commit -am "Updating README"
  [master 5642233] Updating README
   1 file changed, 1 insertion(+)
  ```
1. Now view the log again and observe your new commit at the top:

  ```shell
  $ git log
  commit 564223329b5c6e38024b978c08beeb8907c40477
  Author: John Doe  <x@example.com>
  Date:   Fri Feb 12 14:44:37 2016 -0600
  
      Updating README
  
  commit e3ede2c3777b811feff99eee4a3a456a5030e340
  Author: John Doe  <x@example.com>
  Date:   Fri Feb 12 14:42:31 2016 -0600
  
      Adding README file
  ```
1. Compare the latest commit with the previous one:
  
  ```shell
  $ git diff HEAD^
  diff --git a/README.md b/README.md
  index 2875116..ea66b35 100644
  --- a/README.md
  +++ b/README.md
  @@ -1 +1,2 @@
   The git-busy README file
  +More coming soon...
  ```
1. Check out the previous commit:
  
  ```shell
  $ git checkout HEAD^
  Note: checking out 'HEAD^'.
  
  You are in 'detached HEAD' state. You can look around, make experimental
  changes and commit them, and you can discard any commits you make in this
  state without impacting any branches by performing another checkout.
  
  If you want to create a new branch to retain commits you create, you may
  do so (now or later) by using -b with the checkout command again. Example:
  
    git checkout -b <new-branch-name>
  
  HEAD is now at e3ede2c... Adding README file

  $ cat README.md
  The git-busy README file
  ```
1. Now switch back to the latest commit:
  
  ```shell
  $ git checkout master
  Previous HEAD position was e3ede2c... Adding README file
  Switched to branch 'master'

  $ cat README.md
  The git-busy README file
  More coming soon...
  ```
  
##### Sharing Changes
1. Everything up until this point has been local, but now we want to push it to a remote server. Here, we'll just use a different directory called `remoterepo.git` to emulate the remote server. This would normally be a `ssh` or `https` URL.
  
  ```shell
  $ git init --bare ~/remoterepo.git
  Initialized empty Git repository in ~/remoterepo.git/

  $ git remote add origin ~/remoterepo.git
  ```
1. Now let's view the configured remote repository:
  
  ```shell
  $ git remote -v
  origin  ~/remoterepo.git (fetch)
  origin  ~/remoterepo.git (push)
  ```
1. We'll push our changes to the remote repository so other team members can see them:

  ```shell
  $ git push -u origin master
  Counting objects: 6, done.
  Delta compression using up to 8 threads.
  Compressing objects: 100% (2/2), done.
  Writing objects: 100% (6/6), 517 bytes | 0 bytes/s, done.
  Total 6 (delta 0), reused 0 (delta 0)
  To ~/remoterepo.git
   * [new branch]      master -> master
  Branch master set up to track remote branch master from origin.
  ```
1. Let's clone the repository from the remote URL like a team member would:

  ```shell
  $ git clone ~/remoterepo.git ~/another-busy
  Cloning into '~/another-busy'...
  done.

  $ cd ~/another-busy
  
  $ git log
  commit 564223329b5c6e38024b978c08beeb8907c40477
  Author: John Doe <x@example.com>
  Date:   Fri Feb 12 14:44:37 2016 -0600
  
      Updating README
  
  commit e3ede2c3777b811feff99eee4a3a456a5030e340
  Author: John Doe <x@example.com>
  Date:   Fri Feb 12 14:42:31 2016 -0600
  
      Adding README file
  ```
1. Finally, we'll clean up the cloned repository:
  
  ```shell
  $ cd ~/git-busy
  $ rm -rf ~/another-busy
  ```
##### Branching
1. Branches are very light in git and extremely powerful, let's create one for a new feature we're adding:

  ```shell
  $ git checkout -b feature_x
  ```
1. Next, let's take a look at our branches:

  ```shell
  $ git branch -avv
  ```
Notice that `feature_x` has an asterisk next to it since it is our current branch.  You'll also see the `master` branch which has `origin/master` next to the commit message.  This means that the `master` branch is tracking to the `master` branch on the remote server that we named `origin`. We're not tracking `feature_x` on the remote server.
1. Let's add our feature, an html version of the README file:

  ```shell
  $ cp README.md README.html
  $ git add .
  $ git commit -m "Adding the README in html format"
  ```
1. We decided to make some more changes to the html README:

  ```shell
  $ echo "<h1>Welcome</h1>" >> README.html
  $ git commit -am "Adding welcome message"
  $ git lol
  ```
1. At this point, we're finished with our feature. We want to make sure we're up to date with the latest from the remote repository so let's make sure our local `master` is up to date:

  ```shell
  $ git checkout master
  $ git fetch origin
  $ git merge origin/master
  ```
1. We'll merge the local master into our `feature_x` branch before we merge `feature_x` into `master` so that we can fix any conflicts in our `feature_x` branch, not in `master`:

  ```shell
  $ git checkout feature_x
  $ git merge master
  ```
1. Our `feature_x` branch is now up to date with the latest from `master` so we'll merge it and delete it:

   ```shell
   $ git checkout master
   $ git merge feature_x
   $ git branch -d feature_x
   ```
1. Let's review the log:

  ```shell
  $ git lol
  ```
The feature_x branch is gone and the master branch contains the commit message from our feature branch
1. Let's push our changes upstream to the remote repository so others can pull them down

  ```shell
  $ git push -u origin master
  ```
