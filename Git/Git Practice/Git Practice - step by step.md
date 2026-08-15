# Git Practice Lab — Step by Step

### Step 1 — Initial project

* Create a basic website. ✅
* Add one `<h2>Text</h2>` heading. ✅
* Initialize Git
  * `git init`
* Create the first commit. ✅
  * `git commit -m 'Initial Commit' `
* Push the project to the remote repository. ✅
  * `git push`

### Step 2 — Working on `<span>main</span>`

* Add a h3 to the website. ✅
* Commit the change directly on `<span>main</span>`. ✅
* Push the changes. ✅

### Step 3 — First branch

* Create a new branch. ✅
  * `git switch -c feature/links`
* Add a link to the website. ✅
* Commit the change. ✅
  * `fatal: The current branch feature/links has no upstream branch. To push the current branch and set the remote as upstream, use`
  * To fix this i did: `git push -u origin feature/links`
* Push the branch to the remote repository. ✅

### Step 4 — Merge branch into `<span>main</span>`

* Switch back to `<span>main</span>`. ✅
  * `git branch main`
* Merge the feature branch. ✅
  * `git merge feature/links`
* Push the updated `<span>main</span>`. ✅
  * `git push`

### Step 5 — Multiple branches

* Create two separate branches from `<span>main</span>`. ✅
* Make a different change on each branch. ✅
* Commit both changes separately. ✅
* Push both branches. ✅
  * `git push origin --all`
* Keep both branches independent for now. ✅

### Step 6 — Parallel work on `<span>main</span>` and a branch

* Make a change on a feature branch. ✅
  * `git switch feature/table`
* Commit and push it. ✅
* Switch to `<span>main</span>`. ✅
  * `git switch main`
* Make a different change directly on `<span>main</span>`. ✅
* Commit and push it. ✅
* Observe how the branches now contain different changes. ✅
  * `git log --oneline --graph --all`

### Step 7 — Merge divergent branches

* Take a branch that contains changes not present on `<span>main</span>`. ✅
* Make additional changes on `<span>main</span>`. ✅
* Merge the branch into `<span>main</span>`. ✅
  * `git merge feature/table`
* Observe how Git combines the two different lines of development. ✅

### Step 8 — Merge conflict

* Create a situation where `<span>main</span>` and a feature branch modify the same part of the file differently. ✅
* Attempt to merge the branch. ✅
  * Merge failed and i had to accept manually both changes from different branches.,
* Resolve the conflict manually. ✅
  * Accepted both changes in files
* Complete the merge. ✅
  * `git merge feature/table`
* Push the resolved version. ✅

### Step 9 — Fetch and Pull

* Make changes on the remote repository. ✅
* Update the local repository.  ✅
  * `git fetch` - checks if there were any changes made on remote repo.
  * `git pull` - download all changes and apply them to our local repo.
* Practice the difference between fetching changes and actually integrating them. ✅
* Continue working with the updated project. ✅

### Step 10 — Rebase

* Create a feature branch. ✅
  * `git switch -c feature/homelabImages`
* Make several commits on the branch. ✅
* Make changes to `<span>main</span>` while the branch is being developed. ✅
* Rebase the feature branch onto the updated `<span>main</span>`. ✅
  * `git rebase main` - got error and had to manually accept changes in files.
* Observe how the history changes. ✅
  * Got an error with rebase, had to check all files and add them then use `git rebase --continue`

### Step 11 — Merge vs Rebase

* Create two branches with similar starting points.  ✅
* Integrate one using merge. ✅
* Integrate the other using rebase. ✅
* Compare the resulting Git history. ✅

```
I have failed here because I created branch. RebaseBranch and then instead of switching to main i did another branch here called MergeBranch which got all from RebaseBranch not main.

Have to delete both and redo this excercise.

Switch to main 
`git switch main`

Delete local branches
git branch -D mergeBranch
git branch -D rebaseBranch

Delete them from GitHub
git push origin --delete mergeBranch
git push origin --delete rebaseBranch

```

### Step 12 — Pull Request

* Create a feature branch. ✅
* Develop a small feature on it. ✅
* Push the branch. ✅
  * `git push --set-upstream origin feature/pullFeature`
* Create a Pull Request.
  * ```
    Pull request is not git command, so I have to do it on GitHub website and accept it there after i pushed my new branch with changes from terminal.
    ```
* Review the changes.  ✅
* Merge the Pull Request into `<span>main</span>`. ✅
  * After merging I have deleted this feature branch.

### Step 13 — Pull Request with conflict

* Create a feature branch. ✅
* Make changes on both the branch and `<span>main</span>`. ✅
* Create a Pull Request. ✅
* Cause a conflict. ✅
* Resolve the conflict. ✅
* Complete the Pull Request. ✅

### Step 14 — Final Git workflow

* Start with a clean `<span>main</span>`.
* Create a feature branch.
* Develop a feature through multiple commits.
* Push the branch.
* Keep working on `<span>main</span>` separately.
* Synchronize the branch with `<span>main</span>`.
* Resolve any conflicts.
* Create a Pull Request.
* Merge the feature into `<span>main</span>`.
* Finish with a clean and understandable Git history.
