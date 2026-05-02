# 36 Steps for basic Git/GitHub understanding

## 1\. Introduction

If you need to integrate a project with Git and GitHub and also a fast involvement in this amazing technology, here we have 34 steps for basic Git/GitHub understanding.

## 2\. Requirements

For this example, we need a GitHub account and a Personal access token. 

* In the GitHub Web interface, Click your avatar icon, then Settings. In the left panel, click Developer Settings \- Personal access tokens \- Tokens (classic). Click the “Generate new token” button. In select scopes, click repo  
* We use MacOS operating system, but with some little differences you can use Windows

## 3\. Before we begin

* In the past, the branch master was automatically set up in each Git repository, today **main** is the common.

## 4\. Steps

1. ### **Install Git** 	\- Use the following link: [https://git-scm.com/install](https://git-scm.com/install) for downloading

   1. ### For Mac:

      1. ### If you do not have homebrew, use: [https://brew.sh](https://brew.sh) for installing homebrew

      2. Install Git

	             
		
```shell
$ brew install git  

$ git --version


		git version 2.42.1     
	
``` 

2. ### **Use a folder for our project** t**hen configure Git**, for example: Downloads/Git/laboratorios/lab1, then configure global settings

```shell
# This are global configurations for all Git repositories on your machine
# After this configuration, the changes are stored in .gitconfig in your home directory:
$ ls -la ~
   ...
   .gitconfig
   ...
   $ cd Downloads/Git/laboratorios/lab1
   $ git config --global user.name "Javier Morales"
   $ git config --global user.email "javier.morales@codifika.com.mx"
```


   *NOTE:  You can adjust the settings in each of your repositories to be different from the default data. For this task, use cd to change to the directory in question and run git config again, but this time without the \--global option.*

# Review your configuration settings  
```shell
$ git config --list 
```

3. ### **Create a local repository and the first file**

   
```shell
$ cd Downloads/Git/laboratorios/lab1  
$ git init .  
$ ls -la
   ...  
   .git    
   ...
```

*NOTE:*  
* Using 'master' as the name for the initial branch is not common  
* This default branch name is subject to change. **In step 9 we change from master to main**   
* To configure the initial branch name to use in all of your new repositories, which will suppress this warning, call:  

  		$ git config --global init.defaultBranch <name>*

* Names commonly chosen instead of 'master' are 'main', 'trunk' and 'development'. The just-created branch can be renamed via this command:  

 		 $ git branch -m <name>*

	  
	Create the following file using vi or your preferred editor:

```shell
$ vi Main.java
	public class Main {
	   public static void main(String\[\] args) {
         System.out.println("Hola");
       }
    } 
```

4. ### **Add the file to a repository, review the status untracked**

	
```shell
$ git status
On branch master
No commits yet
Untracked files:
(use "git add <file>..." to include in what will be committed)
			Main.java
nothing added to commit but untracked files present (use "git add" to track) add Main.java
```

```shell
# The file is on stage
$ git add Main.java

$ git status
On branch master
No commits yet

Changes to be committed:
(use "git rm --cached <file>..." to unstage)
			new file:   Main.java  
```

5. ### **Create a commit (snapshot) , so you can restore later. Modify again the same file**

     
*  In Git, a SHA-1 hash is a unique 40-character hexadecimal identifier displayed for every commit  
*  Git commit performs a commit only on the local repository, no data is transferred to an external repository.   
*  **As a best practice, add a short comment for each commit (-m)**  
*  Git commit **displays a “short version” of the SHA-1 hash**, often the first 7 or 8 characters, which is usually sufficient to uniquely identify a commit within a repository.

```shell
$ git commit -m 'initial commit, hello'
[master (root-commit) 382c620\] initial commit, hello
		 1 file changed, 5 insertions(+)
		 create mode 100644 Main.java
$ git status
		On branch master
		nothing to commit, working tree clean 
```
	
```shell
# Create a new file, stage and commit
$ vi Product.java
public class Product {
	private String id;
	private String name;
	private float price;

    public Product(String id, String name, float price) {
       	this.id = id;
    	this.name = name;
		this.price = price;
     }
} 
```
	
```shell
$ git add Product.java
$ git commit -m 'added Product class'  
```

6. ### **View commits**

```shell
# SHA-1 hash is a unique 40-character hexadecimal identifier
# git commit only displays the first 7 characters from SHA-1
$ git log
commit 1d985bcfd97a288eac45e8cd576068ae17a67dd2 (HEAD -> master)
Author: Javier Morales <javier.morales@codifika.com.mx>
Date:   Wed Apr 15 12:22:36 2026 0600
    added Product class
commit 382c6204729e7750027d06bcbae05792d6454369
Author: Javier Morales <javier.morales@codifika.com.mx>
Date:   Wed Apr 15 12:15:28 2026 -0600
initial commit, hello

# Only displays the first 7 characters from SHA-1

$ git log --oneline
	1d985bc added Product class
    382c620 initial commit, hello
```

*NOTE: Here we display the different commits and the last two characters of the short SHA-1 generated by git log –all \-oneline*

*C1<-C2*  
*20 &nbsp;&nbsp;&nbsp;bc*

7. ###  **Exclude files from Git Management**

  a. Create a file .gitignore to exclude files from version control. We are excluding \*.class files and files ending with \*\~ in the following example  
  b. For more information and .gitignore examples:  
     
   [https://github.com/github/gitignore/tree/main](https://github.com/github/gitignore/tree/main)  
   

   
```shell
$ vi .gitignore

# .gitignore file in the repository directory
*.class
*~

$ ls -la
   ...
   .gitignore
   ...

$ git status
On branch master
Untracked files:
(use "git add <file>..." to include in what will be committed)
				.gitignore
nothing added to commit but untracked files present (use "git add" to track) 
```shell
		
```shell
$ git add .gitignore
$ git commit -m "Adding .gitignore"
$ git log --oneline
     da79e82 Adding .gitignore
     1d985bc added Product class
     382c620 initial commit, hello  
```

*NOTE; Here we display the different commits and the last two characters of the short SHA-1 generated by git log –all \-oneline*

*C1\<-C2\<-C3*  
*20&nbsp;&nbsp;&nbsp;&nbsp;bc&nbsp;&nbsp;&nbsp;&nbsp;82*

### **8\. List information about files in the Git index (staging area)**

```shell
$ git ls-files # List files tracked by Git
$ git ls-files --others  # Untracked files
$ git ls-files --stage   # List files tracked by Git, also display: mode (permission mask), object\_name(SHA-1), stage number for every file in the index
```

*NOTE:*

* *Mode:*  
  * *100644: Normal file (non-executable).*  
  * *100755: Executable file.*  
  * *120000: Symbolic link.*  
  * *160000: Submodule.*  
* *Stage (index state)*  
  * *Stage 0: Normal state (no conflicts).*  
  * *Stage 1 (Base): The common ancestor version of the file.*  
  * *Stage 2 (Ours/Target): The version from the branch you are merging into (HEAD).*  
  * *Stage 3 (Theirs/Incoming): The version from the branch being merged*

### **9\. Change branch name from master to main**

```shell
$ git branch -m main  
```

### **10\. Now, as an exercise add a file for example 1\_GitPhases.png and commit with message “Added 1\_GitPhases.png”. Add 2\_Git\_add.png, 3\_States\_file.png and commit with message “2\_… and 3\_… \*.png files added”**

### 

### **11\. Create a branch**

A Git branch is an effective pointer to a snapshot of our changes. When we want to add a new feature or fix a bug (no matter how big or how small is) you spawn a new branch to encapsulate your changes

```shell
# Create a branch
$ git branch my-feature
# List all branches, and we are in main branch (*)
$ git branch
     *main
     my-feature
$ git log

commit 12a2639e3aa25f8c2a0669124b0b410e1da144e1
Author: Javier Morales <javier.morales@codifika.com.mx>
Date:   Wed Apr 15 15:44:07 2026 -0600
     2_... and 3_... *.png files added

commit 67c9b8930f0dad055d6075a42eef1183a0778ca8
Author: Javier Morales <javier.morales@codifika.com.mx>
Date:   Wed Apr 15 15:32:39 2026 -0600
	Added 1_GitPhases.png

commit da79e82c3eac5bd7a2c2c117e90f93250f3f440e
Author: Javier Morales <javier.morales@codifika.com.mx>
Date:   Wed Apr 15 12:50:17 2026 -0600
     Adding .gitignore

commit 1d985bcfd97a288eac45e8cd576068ae17a67dd2
Author: Javier Morales <javier.morales@codifika.com.mx>
Date:   Wed Apr 15 12:22:36 2026 -0600
	added Product class

commit 382c6204729e7750027d06bcbae05792d6454369
Author: Javier Morales <javier.morales@codifika.com.mx>
Date:   Wed Apr 15 12:15:28 2026 -0600
     initial commit, hello  
```

*NOTE; Here we display the different commits and the last two characters of the short SHA-1 generated by git log –all \-oneline*

*C1<-C2<-C3<-C4<-C5*  
*20&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bc&nbsp;&nbsp;&nbsp;&nbsp;82&nbsp;&nbsp;&nbsp;&nbsp;89&nbsp;&nbsp;&nbsp;&nbsp;39*

### **12\. Move to a branch**

	
```shell

$ git checkout my-feature
# Also the following commands display our actual branch
$ git status
	On branch my-feature
	nothing to commit, working tree clean

$ git log
	...
	commit 12a2639e3aa25f8c2a0669124b0b410e1da144e1 (HEAD -> my-feature, main)
	…

$ git branch
	main
	*my-feature
```

*NOTE; Here we display the different commits and the last two characters of the short SHA-1 generated by git log –all \-oneline*

*C1<-C2<-C3<-C4<-C5 (HEAD->myfeature,main)*  
*20&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bc&nbsp;&nbsp;&nbsp;&nbsp;82&nbsp;&nbsp;&nbsp;&nbsp;89&nbsp;&nbsp;&nbsp;&nbsp;39*               

### **13\. We are on branch my-feature, modify and stage a file**

	
```shell
# Add toString method
$ vi Product.java
  ...
  @Override
  public String toString(){
     System.out.println("ID="+id+", NAME="+name+", PRICE="+price);
  }
  ...
$ git status
  On branch my-feature
  Changes not staged for commit:
	(use "git add <file>..." to update what will be committed)
	(use "git restore <file>..." to discard changes in working directory)
	modified:   Product.java
  no changes added to commit (use "git add" and/or "git commit -a") 
```

```shell
$ git add Product.java
$  git status
$ git branch
	main
    *my-feature 
```

### **14\. Commit the change on branch**

	

```shell
$ git commit -m "Add toString() in Product.java"
$ git log
  ...
  commit 71e75f71bb63669da234bc7f06d504cf1b281ebb (HEAD -> my-feature)
	  Add toString() in Product.java
   commit 12a2639e3aa25f8c2a0669124b0b410e1da144e1 (main)
	  2_... and 3_... *.png files added
  ...

$ git branch
	main
    *my-feature

$ cat Product.java
	...
	@Override
    public String toString(){
		System.out.println("ID="+id+", NAME="+name+", PRICE="+price");
    }
   ... 

```

*NOTE; Here we display the different commits and the last two characters of the short SHA-1 generated by git log –all \-oneline*

*C1<-C2<-C3<-C4<-C5 (main)<-C6 (HEAD->myfeature)*  
*20&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bc&nbsp;&nbsp;&nbsp;&nbsp;82&nbsp;&nbsp;&nbsp;&nbsp;89&nbsp;&nbsp;&nbsp;&nbsp;39&emsp;&emsp;&emsp;&emsp;&ensp;&nbsp;f7*

### 

### **15\. Now move to main, verify we do not have the last update, then merge the changes from my-features into main using fast-forward.** 

In fast-forward merge Git just advances the branch pointer to the latest commit of the source branch. No new commits are created, history remains linear and clean. Git defaults to fast-forward merges when possible.

* Advantages  
  * Keeps a very clean commit history  
  * Allows us to see each commit that made up the eventual merged changes, no loss of granularity  
* Disadvantages  
  * Can only be done **when the base branch hasn’t had any new commits**, a rarity in a shared repository  
  * Can be seen as an inaccurate view of history as it hasn’t captured that a branch was created, or when it was merged

	
```shell
# Move to main branch, from here, merge feature
$ git checkout main
$ git log
	...
	commit 12a2639e3aa25f8c2a0669124b0b410e1da144e1 (HEAD -> main)
    Author: Javier Morales <javier.morales@codifika.com.mx>
    Date:   Wed Apr 15 15:44:07 2026 -0600
    	2_... and 3_... *.png files added
	...
```
	
```shell
$ cat Product.java
	...
    Does not have toString() method
    ...

$ git branch
	*main
	my-feature 


```

```shell
# Merge the changes from my-features into main (fast-forward)
$ git checkout main
$ git log --all --oneline
# As we are in main, it receives changes from my-feature branch
$ git merge my-feature
# We have my-feature branch changes into main
$ git branch
	*main
	my-feature 
```

	

```shell
$ cat Product.java
  ...
  @Override
  public String toString(){
	System.out.println("ID="+id+", NAME="+name+", PRICE="+price");
  }
  … 
```

		

### **16\. Review the commits**

```shell
$ git log --all -oneline
   71e75f7 (HEAD -> main, my-feature) Add toString() in Product.java
	12a2639 2_... and 3_... *.png files added
	67c9b89 Added 1_GitPhases.png
	da79e82 Adding .gitignore
	1d985bc added Product class
	382c620 initial commit, hello
```

*NOTE: my-feature is in the same place as main and HEAD, our last commit was fast-forward, so the changes in my-feature were merged with main, so now both are in the same commit. **In step 23 we are going to apply a merge with no fast-forward so you can review the differences.***

*NOTE: Here we display the different commits and the last two characters of the short SHA-1 generated by git log –all \-oneline*  
	  
*C1<-C2<-C3<-C4<-C5<-C6 (**HEAD-> main, my-feature**)*  
*20&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bc&nbsp;&nbsp;&nbsp;&nbsp;82&nbsp;&nbsp;&nbsp;&nbsp;89&nbsp;&nbsp;&nbsp;&nbsp;39&emsp;&nbsp;f7*

### **17\. Remove my-feature branch**

In fast-forward merge, Git simply moves the main pointer forward to include all commits from a feature branch, as we saw in the previous step. That means the commits from the feature branch are now part of main’s history. In this case, deleting a branch only removes the branch pointer, not the commit itself. The work is preserved in main.  
	
```shell
# Remove branch
$ git branch -d my-feature
$ git log --all --oneline
   71e75f7 (HEAD -> main) Add toString() in Product.java
   12a2639 2_... and 3_... *.png files added
   67c9b89 Added 1_GitPhases.png
   da79e82 Adding .gitignore
   1d985bc added Product class
   382c620 initial commit, hello
```

	

### **18\. Review our Git project**

```shell
$ git log --graph --decorate --oneline --all --branches 
```

*NOTE; Here we display the different commits and the last two characters of the short SHA-1 generated by git log –all \-oneline*

*C1<-C2<-C3<-C4<-C5<-C6 (**HEAD-> main**)*  
*20&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bc&nbsp;&nbsp;&nbsp;&nbsp;82&nbsp;&nbsp;&nbsp;&nbsp;89&nbsp;&nbsp;&nbsp;&nbsp;39&emsp;&ensp;f7*

### **19\. Git project name**

Strictly speaking, Git does not have a "project name" field stored within its internal metadata. Instead, what you typically refer to as a "project name" is determined by how it is stored or hosted

    	
```shell
$ basename `git rev-parse --show-toplevel`
    	Lab1 
```

NOTE: When creating a new repository, follow these common conventions:

* No Spaces: Use dashes (-) or underscores (\_) to separate words (e.g., my-cool-project).  
* Lower Case: Most developers prefer all-lowercase names for better compatibility across different operating systems.  
* Descriptive & Brief: Keep it short but clear enough to explain what the project does. 

  ### **20\. Create another branch my-feature2, add changes and commit**

```shell
$ git branch my-feature2
$ git branch
	*main
	my-feature2

$ git checkout my-feature2
$ git branch
	main	
    *my-feature2 
```
```shell
# Modify Product.java
$ vi Product.java
	...
	public String getId(){ return id;}
	... 
```

	
```shell
# Stage
$ git status
$ git add Product.java
$ git status
$ git commit -m "Added getId() into Product.java"
$ git status
$ git log --graph 
```

*NOTE; Here we display the different commits and the last two characters of the short SHA-1 generated by git log –all \-oneline*

*C1<-C2<-C3<-C4<-C5<-C6(main)<-C7(**HEAD-> my-feature2**)*  
*20&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bc&nbsp;&nbsp;&nbsp;&nbsp;82&nbsp;&nbsp;&nbsp;&nbsp;89&nbsp;&nbsp;&nbsp;&nbsp;39&emsp;&ensp;f7&emsp;&emsp;&emsp;&emsp;d8*

### **21\. Add feature2 changes into main using fast-forward merge**

	In this scenario, **we are not going to remove feature2 branch**

```shell
$ git checkout main
# Changes from my-feature2 into main
$ git merge my-feature2
$ git log --graph
	  ....
	  commit fb101d82747865e74a386eb1efc0d6d7d3bfde57 (HEAD -> main, my-feature2)
		| Author: Javier Morales <javier.morales@codifika.com.mx>
    	| Date:   Wed Apr 15 17:39:12 2026 -0600
		|
		|     Added getId() into Product.java
		|
      ....
```

*NOTE; Here we display the different commits and the last two characters of the short SHA-1 generated by git log –all \-oneline*

*C1<-C2<-C3<-C4<-C5<-C6<-C7(**HEAD-> main, my-feature2**)*  
*20&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bc&nbsp;&nbsp;&nbsp;&nbsp;82&nbsp;&nbsp;&nbsp;&nbsp;89&nbsp;&nbsp;&nbsp;&nbsp;39&emsp;&ensp;f7&emsp;&ensp;d8*

### **22\. Add a change in main**

	

```shell
$ git checkout main
$ vi Product.java
    ...
    public String getName() { return name;}
    ...
$ git status
$ git add Product.java
$ git commit -m "Added getName into Product.java" 

```

```shell
$ git log --graph --decorate --oneline --all --branches
	* f4a95ee (HEAD -> main) Added getName into Product.java
	* fb101d8 (my-feature2) Added getId() into Product.java
	* 71e75f7 Add toString() in Product.java
	* 12a2639 2_... and 3_... *.png files added
    * 67c9b89 Added 1_GitPhases.png
	* da79e82 Adding .gitignore
	* 1d985bc added Product class
	* 382c620 initial commit, hello 
```

*NOTE; Here we display the different commits and the last two characters of the short SHA-1 generated by git log –all \-oneline*

*C1<-C2<-C3<-C4<-C5<-C6<-C7(**my-feature2**)<-C8(**HEAD->main**)*  
*20&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;82&nbsp;&nbsp;&nbsp;&nbsp;89&nbsp;&nbsp;&nbsp;&nbsp;39&emsp;&ensp;f7&emsp;&nbsp;d8&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;ee*

### **23\. Create a no-fast-forward merge (or merge commit)**

A no fast-forward merge, using **git merge –no-ff,** so forces a merge commit even if fast-forward is possible. We have an explicit record of the merge but adds an extra commit, sometimes unnecessarily.  
Why use it ?

* Keeps a clean record that a branch was merged  
* Useful for tracking feature integration in collaborative projects  
* Makes it easier to revert or analyze changes later

```shell
# Create a branch
$ git checkout main
$ git branch my-feature3
$ git branch
	* main
  	my-feature2
  	my-feature3

$ git checkout my-feature3
$ git branch
	main
    my-feature2
	*my-feature3
```

```shell
$ vi Product.java
  ...
   public float getPrice() { return price;}
  ...
$ git status
$ git add Product.java
$ git status
$ git commit -m "Added getPrice() into Product.java"
$ git status 
```

```shell
$ git log --graph --decorate --oneline --all --branches

* a095753 (HEAD -> my-feature3) Added getPrice() into Product.java
* f4a95ee (main) Added getName into Product.java
* fb101d8 (my-feature2) Added getId() into Product.java
* 71e75f7 Add toString() in Product.java
* 12a2639 2_... and 3_... *.png files added
* 67c9b89 Added 1_GitPhases.png
* da79e82 Adding .gitignore
* 1d985bc added Product class
* 382c620 initial commit, hello
```

*NOTE; Here we display the different commits and the last two characters of the short SHA-1 generated by git log –all \-oneline. f2 is my-feature2 and f3 is my-feature3, m is main and head is h*

*C1<-C2<-C3<-C4<-C5<-C6<-C7(**f2**)->C8(**m**)->C9(**h->f3**)*  
*20&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bc&nbsp;&nbsp;&nbsp;&nbsp;82&nbsp;&nbsp;&nbsp;&nbsp;89&nbsp;&nbsp;&nbsp;&nbsp;39&emsp;&ensp;f7&emsp;&nbsp;d8&emsp;&emsp;&nbsp;&nbsp;&nbsp;ee&emsp;&emsp;&emsp;53*  
                                                
						     
```shell
$ git checkout main
# Merge feature3 into main using no-fast-forward
$ git merge --no-ff my-feature3 -m "Merge my-feature3 branch into main without fast-forward"

$ git log --graph --decorate --oneline --all --branches
		*   e1f412a (HEAD -> main) Merge my-feature3 branch into main without fast-forward
	    |\
        | \* a095753 (my-feature3) Added getPrice() into Product.java
		|/
     	* f4a95ee Added getName into Product.java
		* fb101d8 (my-feature2) Added getId() into Product.java
		* 71e75f7 Add toString() in Product.java
		* 12a2639 2_... and 3_... *.png files added
		* 67c9b89 Added 1_GitPhases.png
		* da79e82 Adding .gitignore
		* 1d985bc added Product class
		* 382c620 initial commit, hello 
```

*NOTE; Here we display the different commits and the last two characters of the short SHA-1 generated by git log –all \-oneline. f2 is my-feature2 and f3 is my-feature3 and m is main and head is h*

*C1<-C2<-C3<-C4<-C5<-C6<-C7(**f2**)<-C8<-C10(**h->m**)*   
*20&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bc&nbsp;&nbsp;&nbsp;&nbsp;82&nbsp;&nbsp;&nbsp;&nbsp;89&nbsp;&nbsp;&nbsp;&nbsp;39&emsp;&ensp;f7&emsp;&nbsp;d8&emsp;&emsp;&emsp;ee&emsp;2a*    
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|&emsp;&nbsp;|*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|&emsp;&nbsp;v*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|<-C9(**f3**)*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;53*  
                                                                                              

### **24\. Create a remote repository in GitHub**

Using GitHub create a public repository:

- General: jmorales111/lab1demo  
- Description: Test repository  
- Visibility: Public  
- Add README: OFF  
- No .gitignore  
- No license  
- Click “Create repository”

NOTE: DO NOT ADD ANY CONTENT TO THIS REPOSITORY

### **25\. Link our local repository to a remote repository**

```shell
# Replace with your repository URL
$ git remote add origin  https://github.com/jmorales111/lab1demo.git

# If you need to update the URL
$ git remote set-url origin https://github.com/jmorales111/lab1demo.git
# Verification
$ git remote -v 
```

### **26\. Transferring the repository to a remote server github using git push**

```shell
# For avoid error RPC failed; HTTP 400 curl 22 The requested URL returned error: 400
# Set buffer size to 500MB
$ git config --global http.postBuffer 524288000

# -M This is a shortcut for --move --force. It moves (renames) a branch and overrides the safety check that normally prevents you from renaming a branch to a name that is already in use.

$ git branch -M main
$ git push -u origin main
	 	username: <username_not_email>
	 	password: <your_token>
```

### **27\. Connect to GitHub, and verify which branch appears (main, my-feature2, my-feature3)**

In GitHub, click to your avatar icon (right upper corner) \-\> Profile

* Click Repositories tab  
* Click lab1demo  
* Click the main button \-\> View all branches  
  * **It only appears main**  
* We are going to verify in another way, click Code tab \-\> To the right of main button, click "1 Branch button", **\*\*\*it only appears main branch\*\*\***

### **28\. Push other branches**

When you push to GitHub, only the branch you’re currently on gets uploaded unless you explicitly tell Git to send others. That’s why your local branches aren’t showing up.

* Git push without arguments, pushes just the branch you’re on.

	You can use:

```shell
# For a specific branch
$ git push -u origin branch-name

# All branches
$ git push --all origin
```

### **29\. Refresh the GitHub page and review all branches appear**

In GitHub, click to your avatar icon (right upper corner) \-\> Profile

* Click Repositories tab  
* Click lab1demo  
* Click the main button \-\> View all branches  
  * Appears main, my-feature2, my-feature3  
* We are going to verify in another way:  
  * Click Code tab \-\> To the right of main button, click "N Branch button", it appears: main, my-feature2, my-feature3  
  * Click Code tab, then click Insights  
    * In the left panel, click Network

### **30\. Create and make active a new branch and add commit a change**

Use \-b when you checkout a branch, **it creates the branch and references to it (HEAD points to it)**

	

```shell
$ git checkout -b my-feature4
# Modify Product.java
...
public void setPrice(float price) {
      this.price = price;
}
...
```


```shell
$ git add Product.java
$ git commit -m "Added setPrice() into Product.java"
$ git status
$ git log --graph --decorate --oneline --all --branches 
```

*NOTE; Here we display the different commits and the last two characters of the short SHA-1 generated by git log –all \-oneline. f2 is my-feature2, f3 is my-feature3, m is main, head is h. Since we just synchronize with GitHub, origin is the remote URL, identified with o.*

*C1<-C2<-C3<-C4<-C5<-C6<-C7(o/f2,f2)<-C8<-C10(m)*  
*20&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bc&nbsp;&nbsp;&nbsp;&nbsp;82&nbsp;&nbsp;&nbsp;&nbsp;89&nbsp;&nbsp;&nbsp;&nbsp;39&emsp;&ensp;f7&emsp;&nbsp;d8&emsp;&emsp;&emsp;ee&emsp;2a*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|&emsp;&nbsp;&nbsp;|<-C11(h->f4)*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|&emsp;&nbsp;&nbsp;|&emsp;&nbsp;&nbsp;74*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|&emsp;&nbsp;v*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|<-C9(o/f3,f3)*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;&nbsp;&nbsp;53*

### 

### **31\. Suppose we modify many files, create a new folder, move some files, delete some files using the previous branch (my-feature4)**

	

```shell
$ git status
$ mkdir info
$ mv *.png info/

# We rename and add png files to info
# We stage a folder
$ git add info

# Stage all new, modified and deleted files in current directory
$ git add -A

$ git status
Changes to be committed:
		  (use "git restore --staged \<file\>..." to unstage)
			modified:   .gitignore
     		new file:   info/0_What is version control.png
			new file:   info/1_Git.png
			new file:   info/2_Local_Remote_Repositories.png
			renamed:    1_GitPhases.png -> info/3_GitPhases.png
			new file:   info/5_Git_Init.png
			new file:   info/6_Git_add_Git_commit.png
			renamed:    2_Git_add.png -> info/7_Git_add.png
			renamed:    3_States_File.png -> info/8_States_File.png
			new file:   info/9_Git_commit.png 
```

	
```shell
$ git branch
    main
    my-feature2
	my-feature3
	* my-feature4 
```

### **32\. Commit new additional changes in my-feature4 and review the structure**

	
```shell
$ git commit -m "Move png files to folder info, add,remove files in info folder, modify .gitignore"
$ git status
	On branch my-feature4
	nothing to commit, working tree clean
```

	
```shell
$ git log --graph --decorate --oneline --all --branches
* 367eb2b (HEAD -> my-feature4) Move png files to folder info, add,remove files in info folder, modify .gitignore
* b83b874 Added setPrice() into Product.java
*   e1f412a (origin/main, main) Merge my-feature3 branch into main without fast-forward
|\
| * a095753 (origin/my-feature3, my-feature3) Added getPrice() into Product.java
|/
* f4a95ee Added getName into Product.java
* fb101d8 (origin/my-feature2, my-feature2) Added getId() into Product.java
* 71e75f7 Add toString() in Product.java
* 12a2639 2_... and 3_... \*.png files added
* 67c9b89 Added 1_GitPhases.png
* da79e82 Adding .gitignore
* 1d985bc added Product class
* 382c620 initial commit, hello 
```


*NOTE; Here we display the different commits and the last two characters of the short SHA-1 generated by git log –all \-oneline. f2 is my-feature2, f3 is my-feature3, m is main, head is h. Since we just synchronize with GitHub, origin is the remote URL, identified with o.*

*C1<-C2<-C3<-C4<-C5<-C6<-C7(o/f2,f2)<-C8<-C10(**o/m,m**)*  
*20&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bc&nbsp;&nbsp;&nbsp;&nbsp;82&nbsp;&nbsp;&nbsp;&nbsp;89&nbsp;&nbsp;&nbsp;&nbsp;39&emsp;&ensp;f7&emsp;&nbsp;d8&emsp;&emsp;&emsp;ee&emsp;2a*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|&emsp;&nbsp;&nbsp;|<-C11<-C12(**h->f4**)*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|&emsp;&nbsp;&nbsp;|&emsp;&nbsp;74&emsp;&nbsp;2b*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|&emsp;&nbsp;&nbsp;v*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|<-C9(o/f3,f3)*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;&nbsp;53*

### **33\. Push to GitHub after creating a branch**

	  
	
```shell
$ git push

fatal: The current branch my-feature4 has no upstream branch.
		To push the current branch and set the remote as upstream, use
	   		git push --set-upstream origin my-feature4

To have this happen automatically for branches without a tracking upstream, see 'push.autoSetupRemote' in 'git help config'.
```

*NOTE: The error message indicates the correct procedure: You must use the \--set-upstream option or \-u to specify that the already known origin repository (i.e., origin) should also be used for the new branch:*

	
```shell
$ git push --set-upstream origin my-feature4

Enumerating objects: 16, done.
Counting objects: 100% (16/16), done.
Delta compression using up to 8 threads
Compressing objects: 100% (13/13), done.
Writing objects: 100% (13/13), 2.92 MiB | 41.58 MiB/s, done.
Total 13 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0\)

remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
remote:
remote: Create a pull request for 'my-feature4' on GitHub by visiting:

remote:      https://github.com/jmorales111/lab1demo/pull/new/my-feature4
remote:
To https://github.com/jmorales111/lab1demo.git
	* \[new branch\]      my-feature4 -> my-feature4
	branch 'my-feature4' set up to track 'origin/my-feature4'.

$ git log --graph --decorate --oneline --all --branches
          * 367eb2b (HEAD -> my-feature4, origin/my-feature4)   Move png files to folder info, add,remove files in info folder, modify .gitignore
		  * b83b874 Added setPrice() into Product.java
          *   e1f412a (origin/main, main) Merge my-feature3 branch into main without fast-forward
		  |\
          | * a095753 (origin/my-feature3, my-feature3) Added getPrice() into Product.java
          |/
		  * f4a95ee Added getName into Product.java
		  * fb101d8 (origin/my-feature2, my-feature2) Added getId() into Product.java
 		  * 71e75f7 Add toString() in Product.java
          * 12a2639 2_... and 3_... \*.png files added
          * 67c9b89 Added 1_GitPhases.png
          * da79e82 Adding .gitignore
          * 1d985bc added Product class
		  * 382c620 initial commit, hello
```

*NOTE; Here we display the different commits and the last two characters of the short SHA-1 generated by git log –all \-oneline. f2 is my-feature2, f3 is my-feature3, m is main, head is h. Since we just synchronize with GitHub, origin is the remote URL, identified with o.*

*C1<-C2<-C3<-C4<-C5<-C6<-C7(o/f2,f2)<-C8<-C10(**o/m,m**)*  
*20&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bc&nbsp;&nbsp;&nbsp;&nbsp;82&nbsp;&nbsp;&nbsp;&nbsp;89&nbsp;&nbsp;&nbsp;&nbsp;39&emsp;&ensp;f7&emsp;&nbsp;d8&emsp;&emsp;&emsp;ee&emsp;2a*   
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|&emsp;&nbsp;&nbsp;|<-C11<-C12(**h->f4,o/f4**)*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|&emsp;&nbsp;&nbsp;|&emsp;74&emsp;&emsp;2b*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|&emsp;&nbsp;&nbsp;v*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|<-C9(o/f3,f3)*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;&nbsp;53*  

```shell
# Open the gitHub page, at main branch we do not have the last changes because we have not merge, but if you choose my-feature4, you will see this last changes

# At command line review the changes
$ git checkout my-feature4
$ ls
$ ls info
	...	0_What is version control.png
		1_Git.png
	...
# Review files in main branch
$ git checkout main

# The info folder is not displayed, we have not merge my-feature4
$ ls 
```

	
```shell
# List of commits
$ git log --oneline
	e1f412a (HEAD -> main, origin/main) Merge my-feature3 branch into main without fast-forward
	a095753 (origin/my-feature3, my-feature3) Added getPrice() into Product.java
	f4a95ee Added getName into Product.java
	fb101d8 (origin/my-feature2, my-feature2) Added getId() into Product.java
	71e75f7 Add toString() in Product.java
	12a2639 2_... and 3_... *.png files added
	67c9b89 Added 1_GitPhases.png
	da79e82 Adding .gitignore
	1d985bc added Product class
	382c620 initial commit, hello |
```

	 

### **34\. Git Cherry pick** 

Is the act of **picking a commit from a branch and applying it to another**. git cherry-pick can be useful for undoing changes. For example, say a commit is accidently made to the wrong branch. You can switch to the correct branch and cherry-pick the commit to where it should belong.  
	  
Git cherry-pick is a useful tool but not always a best practice. Cherry	picking can cause duplicate commits and many scenarios where cherry picking would work, traditional merges are preferred instead. With that said git cherry-pick is a handy tool for a few scenarios…

SEE: <https://www.atlassian.com/git/tutorials/cherry-pick](https://www.atlassian.com/git/tutorials/cherry-pick>

**We use a cherry pick to bring changes to main using my-feature4 last commit (without a merge)**

```shell
# List of commits
$ git log --oneline
	e1f412a (HEAD -> main, origin/main) Merge my-feature3 branch into main without fast-forward
	a095753 (origin/my-feature3, my-feature3) Added getPrice() into Product.java
	f4a95ee Added getName into Product.java
	fb101d8 (origin/my-feature2, my-feature2) Added getId() into Product.java
	71e75f7 Add toString() in Product.java
	12a2639 2_... and 3_... *.png files added
	67c9b89 Added 1_GitPhases.png
	da79e82 Adding .gitignore
	1d985bc added Product class
	382c620 initial commit, hello |
```

	
```shell
# List all commits and braches
$ git log --graph --decorate --oneline --all --branches

		* 367eb2b (origin/my-feature4, my-feature4) Move png files to folder info, add,remove files in info folder, modify .gitignore
	    * b83b874 Added setPrice() into Product.java
	    * e1f412a (HEAD -> main, origin/main) Merge my-feature3 branch into main without fast-forward
		|\
		| \* a095753 (origin/my-feature3, my-feature3) Added getPrice() into Product.java
		|/
		* f4a95ee Added getName into Product.java
        * fb101d8 (origin/my-feature2, my-feature2) Added getId() into Product.java
		* 71e75f7 Add toString() in Product.java
		* 12a2639 2_... and 3_... *.png files added
		* 67c9b89 Added 1_GitPhases.png
		* da79e82 Adding .gitignore
        * 1d985bc added Product class
		* 382c620 initial commit, hello |
```

NOTE: Review the differences in the output, with the last two commands

	
```shell
# In the following steps, the changes in my-feature4 branch, added to main (without a merge)
$ git checkout main 
```

    
```shell
# Cherry-pick
# 367eb2b is the my-feature4 SHA-1 or commit reference
$ git cherry-pick 367eb2b

		main c35ebd8] Move png files to folder info, add,remove files in info folder, modify .gitignore
		 Date: Fri Apr 17 11:22:00 2026 -0600
		 10 files changed, 22 insertions(+)
		 create mode 100644 info/0_What is version control.png
		 create mode 100644 info/1_Git.png
		 create mode 100644 info/2_Local_Remote_Repositories.png
		 rename 1_GitPhases.png => info/3_GitPhases.png (100%)
		 create mode 100644 info/5_Git\_Init.png
		 create mode 100644 info/6_Git_add_Git_commit.png
		 rename 2_Git_add.png => info/7_Git_add.png (100%)
    	 rename 3_States_File.png => info/8_States_File.png (100%)
		 create mode 100644 info/9__Git_commit.png
```

	
```shell
$ git log --graph --decorate --oneline --all --branches

* c35ebd8 (HEAD -> main) Move png files to folder info, add,remove files in info folder, modify .gitignore
| * 367eb2b (origin/my-feature4, my-feature4) Move png files to folder info, add,remove files in info folder, modify .gitignore
| * b83b874 Added setPrice() into Product.java|/\*   e1f412a (origin/main) Merge my-feature3 branch into main without fast-forward|\\| \* a095753 (origin/my-feature3, my-feature3) Added getPrice() into Product.java|/\* f4a95ee Added getName into Product.java\* fb101d8 (origin/my-feature2, my-feature2) Added getId() into Product.java\* 71e75f7 Add toString() in Product.java\* 12a2639 2\_... and 3\_... \*.png files added\* 67c9b89 Added 1\_GitPhases.png\* da79e82 Adding .gitignore\* 1d985bc added Product class\* 382c620 initial commit, hello |
| :---- |
```

*NOTE: Review the first row of the previous output, this is the cherry-pick, the commit on my-feature4 is added to main branch, **but my-feature4 is not merged, so continues as a branch***

### **35\. Use GitHub, push  and review the changes**

```shell
# All branches
$ git push --all origin
	Enumerating objects: 12, done.
    Counting objects: 100% (12/12), done.
	Delta compression using up to 8 threads
	Compressing objects: 100% (10/10), done.
	Writing objects: 100% (10/10), 2.92 MiB | 41.01 MiB/s, done.
	Total 10 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0\)
	To https://github.com/jmorales111/lab1demo.git
	   e1f412a..c35ebd8  main \-\> main |
```

\- In GitHub, click to your avatar icon (right upper corner) -> Profile

* Click Repositories tab  
* Click lab1demo  
* Click the main button \-\> View all branches  
  * Appears main, my-feature2, my-feature3, my-feature4

    

\- We are going to verify in another way:

* Click Code tab \-\> To the right of main button, click "N Branch button", it appears: main, my-feature2, my-feature3, my-feature4  
* Click Code tab, then click Insights  
  * In the left panel, click Network

    

\- In main branch, you should have a info folder, new files and updated files into info folder after the cherry pick  
	\- So we have the following according to: git log \--graph \--decorate \--oneline \--all \--branches  
	\- The numeric value are the last two digits from SHA-1  
	\- fn is a feature

		   

C1<-C2<-C3<-C4<-C5<-C6<-C7(**o/f2,f2**)<-C8<-C10<-C13 (**h-\>m,o/m**)  
*20&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bc&nbsp;&nbsp;&nbsp;&nbsp;82&nbsp;&nbsp;&nbsp;&nbsp;89&nbsp;&nbsp;&nbsp;&nbsp;39&emsp;&ensp;f7&emsp;&nbsp;d8&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;ee&emsp;&nbsp;2a&emsp;&nbsp;&nbsp;d8*   
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|&emsp;&emsp;&nbsp;&nbsp;|<-C11<-C12(**h->f4,o/f4**)*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|&emsp;&emsp;&nbsp;&nbsp;|&emsp;&ensp;74&emsp;&ensp;2b*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|&emsp;&emsp;&nbsp;&nbsp;v*  
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;|<-C9(**o/f3,f3**)*    
*&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;&nbsp;53*

### **36\. Open your project using Visual Studio Code Editor**

	In Visual Studio Code Editor, add the following extension:  
	![][image1]

- In Visual Studio Code Editor, go to File menu-Open Folder…. Navigate to our project folder Downloads/Git/laboratorios/lab1  
- In the lower left area, click Git Graph

![][image2]

- Review all Git changes:

![][image3]

### **37\. Rename remote repository**

1. In GitHub rename the repository from lab1demo to gitbasics   
2. In GitHub, click to your avatar icon (right upper corner) \-\> Profile  
* Click Repositories tab  
* Click lab1demo  
* In the upper right corner, click Settings icon (gear)  
  * In General section, in repository name, remove lab1demo and replace with git\_basics  
  * Click Rename button  
* Now the URL is: https://github.com/jmorales111/git\_basics.git  
3. With a  terminal, change to your working directory:  
     
     
     
     
     
     
     
   
```shell
$ cd Downloads/Git/laboratorios/lab1
# Displays the old URL
$ git remote -v
# Update the URL
$ git remote set-url origin https://github.com/jmorales111/git\_basics.git
$ git remote -v 
```

*NOTES:* 

- *Collaborators: They’ll also need to update the remotes if they cloned using the old URL*  
- *CI/CD pipelines: Update any scripts, deployments configs, or integrations that reference the old repo name*  
- *Webhooks & API calls: Check if they use hardcoded URLs*


### **38\. Update the repository**

Copy some files and create the [README.md](http://README.md) in the local repository

```shell
$ git checkout main
$ git status
# Add [README.md](http://README.md) and other files in info directory
$ git add \-A
$ git status
$ git commit -m "README.md and other files in info directory added"
$ git log --graph --decorate --oneline --all --branches
# All branches
$ git push --all origin
```

## 5\. Best practices

In production projects, the best Git branching practices center on maintaining stability, traceability, and controlled integration. The most effective workflows are [GitFlow](https://www.gitkraken.com/learn/git/git-flow), [Trunk‑Based Development](https://www.gitkraken.com/blog/trunk-based-development), and [GitHub Flow](https://medium.com/@yanminthwin/understanding-github-flow-and-git-flow-957bc6e12220), each balancing speed and safety depending on release frequency and team size.

1. **Protect the main branch**  
   1. Keep main (or master) always deployable  
   2. Use branch protection rules: require pull-request reviews, CI (Continuous Integration) checks, and no direct pushes  
   3. Tag releases with semantic versioning (v1.2.3) for traceability  
2. **Use short-lived feature branches**  
   1. Create branches for each feature of bug fix  
   2. Merge back quickly (within days) to avoid drift and conflicts  
   3. Delete branches after merging to keep the repo clean  
3. **Integrate continuously**  
   1. Automate builds and test on every pull request  
   2. Use CI/CD pipelines to deploy staging environments before production  
   3. Merge only when test pass and code reviews are complete  
4. **Separate environments**  
   1. Maintain distinct branches for development, staging, and production if you release process demands it, for example:  
      1. Develop \-\> integration testing  
      2. release/x.y \-\> pre-production  
      3. Main \-\> production deployment  
5. **Best practices for production stability**  
   1. Tag releases: Use annotated tags for production versions  
   2. Hotfix branches: Create hotfix/\* for urgent production fixes, merge back to both main and develop  
   3. Code reviews: Mandatory before merging to production  
   4. Automated testing: Unit, integration, and regression test must run before deployment  
   5. Documentation: Maintain clear commit messages and changelogs for auditability

	

**Popular branching models**

	

| Strategy | Ideal for | Key Branches | Pros | Cons |
| :---- | :---- | :---- | :---- | :---- |
| GitFlow | Large teams, scheduled releases | main, develop, feature/\*, release/\*, hotfix/\* | Clear structure, supports parallel work | Heavy for fast‑moving projects |
| GitHub Flow | Continuous deployment | main, feature/\* | Simple, fast, great for web apps | Risky without strong CI/CD |
| Trunk‑Based Development | High‑velocity teams | main only, short feature branches | Minimal merge conflicts, fast delivery  | Requires disciplined testing |
| Release Flow (Microsoft) | Enterprise CI/CD | main, release/\*, hotfix/\* | Stable releases, rollback support Slightly complex setup | Slightly complex setup |

## 6\. Additional resources

* [https://github.com/github/gitignore/tree/main](https://github.com/github/gitignore/tree/main)

* [https://iterm2.com](https://iterm2.com)

* [https://www.atlassian.com/git/tutorials/cherry-pick](https://www.atlassian.com/git/tutorials/cherry-pick)

* [https://learngitbranching.js.org](https://learngitbranching.js.org)  
* [https://www.gitkraken.com/learn/git/git-flow](https://www.gitkraken.com/learn/git/git-flow)  
* [https://www.gitkraken.com/blog/trunk-based-development](https://www.gitkraken.com/blog/trunk-based-development)  
* [https://medium.com/@yanminthwin/understanding-github-flow-and-git-flow-957bc6e12220](https://medium.com/@yanminthwin/understanding-github-flow-and-git-flow-957bc6e12220)
