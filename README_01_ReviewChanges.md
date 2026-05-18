# Review changes between different commits
<br/>
<br/>

## 1\. List commits
```shell
$ git log --graph --decorate --oneline --all --branches
```
```text
   ...
   * da79e82 Adding .gitignore
   * 1d985bc added Product class
   * 382c620 initial commit, hello
```
<br/>
<br/>

## 2\. In the first commit , how were the files?
```shell
# SHA-1 for the first commit
$ git checkout 382c620
$ ls
    ...
    Main.java
    ...
$ cat Main.java
public class Main {
  public static void main(String[] args) {
    System.out.println("Hola");
  }
}

$ git log --graph --decorate --oneline --all --branches
...
 160a627 (origin/main, origin/HEAD, main) Add cheat-sheet1-Git.pdf
...
* 382c620 (HEAD) initial commit, hello
...
```
*NOTE: We display the first and last commit. HEAD points to the commit we move to, and main points to the last commit. The remote main and HEAD (origin/main and origin/HEAD) points to the latest commit*

<br/>

## 3\. Return to the last commit ##
```shell
$ git checkout main
```

<br/>
<br/>

## 4\. Undo changes after stage ##

### a\. Add a setName method ###
```shell
$ vi Product.java
...
public void setName(String name) {this.name=name;}
...
```
### b\. Stage the change ###
```shell
$ git status
$ git add Product.java
```
### c\. Unstage the change (remove it from staging area without losing your local changes) ###
```shell
# For Git >=2.23.0
$ git restore --staged Product.java
$ git status
# We have the setName() method
$ cat Product.java
```
### d\. Unstage the change (remove it from staging area and delete changes) ###
```shell
# We have the setName() method
$ cat Product.java

# Stage the change
$ git add Product.java
$ git status

# Unstage and delete changes
$ git checkout HEAD -- Product.java
$ git status

# The method setName() does not appear
$ cat Product.java
```

## 4\. Undo changes after commit, without pushed yet ##
### a\. Add a setName method ###
```shell
$ vi Product.java
...
public void setName(String name) {this.name=name;}
...
```
### b\. Stage the change ###
```shell
$ git status
$ git add Product.java
```
### c\. commit the change ###
```shell
$ git commit -m "Add setName in Product.java"
$ git status
```
### d\. Undo commit but keep changes in stage (Safe) ###
```shell
# Review the last commit
$ git log --oneline
    623feaa (HEAD -> main) Add setName in Product.java
    ...

# Undo commit, but keep your files exactly as they are in the staging (ready to be committed again)
$ git reset --soft HEAD~1

# Product.java is again in stage
$ git status
# The changes appear again
$ cat Product.java
...
 public void setName(String name) {this.name=name;}
...

# The last commit is removed
$ git log --oneline

# Commit the changes, for the next step
$ git commit -m "Add setName, in Product.java, second execution"
$ git log --oneline
```

### e\. Undo commit and unstage changes (changes are in working directory) ###
```shell
# Review the last commit
$ git log --oneline
    546a83c (HEAD -> main) Add setName, in Product.java, second execution

# This removes the commit and moves the changes back to your working directory 
$ git reset HEAD~1

# Product.java it is not in stage
$ git status

# The changes appear again
$ cat Product.java
...
 public void setName(String name) {this.name=name;}
...

# For the next step, commit the changes
$ git add Product.java
$ git commit -m "Add setName, in Product.java, third execution"
$ git log --oneline
```
### f\. Undo commit and delete changes (permanent)  ###
```shell
# Review the last commit
$ git log --oneline
    a914f0f (HEAD -> main) Add setName, in Product.java, third execution
...
# Warning: This completely deletes your code changes from that commit
$ git reset --hard HEAD~1

# Product.java is not in stage
# Product.java is in the working directory, but the changes are lost
$ git status

# setName() method does not appear
$ cat Product.java
```
<br/>
<br/>

## 5\. Undo changes after commit and push ##

### a\. Add a setName method ###
```shell
$ vi Product.java
...
public void setName(String name) {this.name=name;}
...
```
### b\. Stage the change ###
```shell
$ git status
$ git add Product.java
$ git log --oneline
$ git commit -m "Add setName, in Product.java, fourth execution"
$ git log --oneline
```
### c\. Push the change ###
*If others use the same repository, you should not "delete" history. Instead, create a new commit that does the exact opposite of the bad one using git revert*

```shell
$ git push
$ git status
```
### d\. Find the last commit SHA-1
```shell
# Find the last commit, for our example 369899b
$ git log --graph --decorate --oneline --all --branches

* 369899b (HEAD -> main, origin/main, origin/HEAD) Add setName, in Product.java, fourth execution
...
```
### e\. Revert the commit
```shell
$ git revert 369899b
# The changes are removed
# The setName() does not appear
$ cat Product.java
```
*NOTE: If the vi editor appears, you can add a comment, or simple write an exits using wq*

### f\. Push the fix
```shell
$ git push origin main
```
### g\. Review the log
```shell
$ git log --graph --decorate --oneline --all --branches

* 2d241c5 (HEAD -> main, origin/main, origin/HEAD) Revert "Add setName, in Product.java, fourth execution"
* 369899b Add setName, in Product.java, fourth execution
...
```
<br/>
<br/>

## 6\. Modify the most recent commit in our current branch ##
*It effectively replaces the last commit with a new one that combines any new staged changes with the previous commit's content*
### a\. Modify last commit message
```shell
# If you made a typo or want to reword the last message, running git commit --amend will open your default editor to update the text.
# Change 
# Revert "Add setName, in Product.java, fourth execution" to 
# Revert "Add setName(), in Product.java, fourth execution"
# ESC + :wq

$ git commit --amend
$ git log --graph --decorate --oneline --all --branches

* 19c3b64 (HEAD -> main) Revert "Add setName(), in Product.java, fourth execution"
| * 2d241c5 (origin/main, origin/HEAD) Revert "Add setName, in Product.java, fourth execution"
|/
* 369899b Add setName, in Product.java, fourth execution
```
*NOTE:*
- *Amend commits are actually entirely new commits (19c3b64) and the previous commit (2d241c5) will no longer be on our current branch*
- *Avoid amending a commit that other developers have based the work on*

### b\. Add a forgotten file
*If you forgot to include a file, you can stage it with git add <file> and then run git commit --amend to "tuck" it into the last commit instead of creating a new one.*.  
*Add the following files: info/21_Different_Methods_Record_Changes, info/22_Amend.png, info/23_Amend.png*

```shell
$ git status
# Stage new files
$ git add info/21_Different_Methods_Record_Changes.png
$ git add info/22_Amend.png
$ git add info/23_Amend.png

# Include this changes in the last commit

# Running git commit --amend will open your default editor to update the text.
# Change 
# Revert "Add setName(), in Product.java, fourth execution" to 
# Revert "Add setName(), in Product.java, fourth execution and add info/21 to info/23 files"
# ESC + :wq
$ git commit --amend
```
```shell
$ git log --graph --decorate --oneline --all --branches
* 67e3642 (HEAD -> main) Revert "Add setName(), in Product.java, fourth execution and add info/21 to info/23 files"
| * 2d241c5 (origin/main, origin/HEAD) Revert "Add setName, in Product.java, fourth execution"
|/
* 369899b Add setName, in Product.java, fourth execution
...
```
*NOTE:*
- *The last commit with different SHA-1 as the previous one, after the amend*

### c\. Push the changes
```shell
$ git push


To https://github.com/jmorales111/git_basics.git
 ! [rejected]        main -> main (non-fast-forward)
error: failed to push some refs to 'https://github.com/jmorales111/git_basics.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. If you want to integrate the remote changes,
hint: use 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
```shell
```













