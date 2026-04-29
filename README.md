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
	* *Using 'master' as the name for the initial branch is not common*  
	* *This default branch name is subject to change. **In step 9 we change from master to main***  
	* *To configure the initial branch name to use in all of your new repositories, which will suppress this warning, call:*

  		*$ git config --global init.defaultBranch <name>*

	* *Names commonly chosen instead of 'master' are 'main', 'trunk' and 'development'. The just-created branch can be renamed via this command:*

 		 *git branch -m <name>*

	  
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
(use "git add \<file\>..." to include in what will be committed)
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
(use "git rm \--cached \<file\>..." to unstage)
			new file:   Main.java  
```

5. ### **Create a commit (snapshot) , so you can restore later. Modify again the same file**

     
* In Git, a SHA-1 hash is a unique 40-character hexadecimal identifier displayed for every commit  
* Git commit performs a commit only on the local repository, no data is transferred to an external repository.   
* **As a best practice, add a short comment for each commit (-m)**  
* Git commit **displays a “short version” of the SHA-1 hash**, often the first 7 or 8 characters, which is usually sufficient to uniquely identify a commit within a repository.

```shell
$ git commit \-m 'initial commit, hello'
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
commit 1d985bcfd97a288eac45e8cd576068ae17a67dd2 (HEAD \-\> master)
Author: Javier Morales <javier.morales@codifika.com.mx>
Date:   Wed Apr 15 12:22:36 2026 0600
    added Product class
commit 382c6204729e7750027d06bcbae05792d6454369
Author: Javier Morales \<javier.morales@codifika.com.mx\>
Date:   Wed Apr 15 12:15:28 2026 -0600
initial commit, hello

# Only displays the first 7 characters from SHA-1

$ git log \--oneline
	1d985bc added Product class
    382c620 initial commit, hello
```

*NOTE; Here we display the different commits and the last two characters of the short SHA-1 generated by git log –all \-oneline*

*C1\<-C2*  
*20    bc*

7. ###  **Exclude files from Git Management**

1. Create a file .gitignore to exclude files from version control. We are excluding \*.class files and files ending with \*\~ in the following example  
2. For more information and .gitignore examples:  
     
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
(use "git add \<file\>..." to include in what will be committed)
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
*20    bc    82*

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

*C1\<-C2\<-C3\<-C4\<-C5*  
*20    bc    82    89    39*

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

*C1\<-C2\<-C3\<-C4\<-C5 (HEAD-\>myfeature,main)*  
*20    bc    82    89    39*               

### **13\. We are on branch my-feature, modify and stage a file**

	
```shell
# Add toString method
$ vi Product.java
  ...
  @Override
  public String toString(){
     System.out.println("ID="+id+", NAME="+name+", PRICE="+price");
  }
  ...
$ git status
  On branch my-feature
  Changes not staged for commit:
	(use "git add \<file\>..." to update what will be committed)
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

*C1\<-C2\<-C3\<-C4\<-C5 (main)\<-C6 (HEAD-\>myfeature)*  
*20    bc    82    89    39               f7*

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

*NOTE; Here we display the different commits and the last two characters of the short SHA-1 generated by git log –all \-oneline*  
	  
*C1\<-C2\<-C3\<-C4\<-C5\<-C6 (**HEAD-\> main, my-feature**)*  
*20    bc    82    89    39    f7*

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

*C1\<-C2\<-C3\<-C4\<-C5\<-C6 (**HEAD-\> main**)*  
*20    bc    82    89    39    f7*

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

*C1\<-C2\<-C3\<-C4\<-C5\<-C6(main)\<-C7(**HEAD-\> my-feature2**)*  
*20    bc    82    89    39    f7               d8*

### **21\. Add feature2 changes into main using fast-forward merge**

	In this scenario, **we are not going to remove feature2 branch**

```shell
$ git checkout main
# Changes from my-feature2 into main
$ git merge my-feature2
$ git log --graph
	  ....
	  commit fb101d82747865e74a386eb1efc0d6d7d3bfde57 (HEAD -> main, my-feature2)
		| Author: Javier Morales <javier.morales@codifika.com.mx\>
    	| Date:   Wed Apr 15 17:39:12 2026 -0600
		|
		|     Added getId() into Product.java
		|
      ....
```

*NOTE; Here we display the different commits and the last two characters of the short SHA-1 generated by git log –all \-oneline*

*C1\<-C2\<-C3\<-C4\<-C5\<-C6\<-C7(**HEAD-\> main, my-feature2**)*  
*20    bc    82    89    39    f7     d8*

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

*C1\<-C2\<-C3\<-C4\<-C5\<-C6\<-C7(**my-feature2**)\<-C8(**HEAD-\>main**)*  
*20    bc    82    89    39    f7     d8                          ee*

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

*C1\<-C2\<-C3\<-C4\<-C5\<-C6\<-C7(**f2**)-\>C8(**m**)-\>C9(**h-\>f3**)*  
*20    bc    82    89    39    f7     d8          ee        53*  
                                                
						     
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

*C1\<-C2\<-C3\<-C4\<-C5\<-C6\<-C7(**f2**)\<-C8\<-C10(**h-\>m**)*   
*20    bc    82    89    39    f7     d8          ee      2a*    
                                                              *|         |*  
                                                              *|         v*  
                                                              *|\<-C9(**f3**)*  
                                                                  *53*  
                                                                                              

### **24\. Create a remote repository in GitHub**

	Using GitHub create a public repository:

		\- General: jmorales111/lab1demo  
		\- Description: Test repository  
		\- Visibility: Public  
		\- Add README: OFF  
		\- No .gitignore  
		\- No license  
		\- Click “Create repository”

		NOTE: DO NOT ADD ANY CONTENT TO THIS REPOSITORY

### **25\. Link our local repository to a remote repository**

```shell
# Replace with your repository URL
$ git remote add origin  https://github.com/jmorales111/lab1demo.git

# If you need to update the URL
$ git remote set\-url origin https://github.com/jmorales111/lab1demo.git
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
	 	username: <username not email\>
	 	password: <your\_token\>
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

\# All branches
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

*C1\<-C2\<-C3\<-C4\<-C5\<-C6\<-C7(o/f2,f2)\<-C8\<-C10(m)*  
*20    bc    82    89    39    f7     d8                 ee   2a*    
                                                                      *|      |\<-C11(h-\>f4)*  
                                                                      *|      |     74*   
                                                                      *|      |*  
                                                                      *|\<-C9(o/f3,f3)*  
                                                                           *53*

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

*C1\<-C2\<-C3\<-C4\<-C5\<-C6\<-C7(o/f2,f2)\<-C8\<-C10(**o/m,m**)*  
*20    bc    82    89    39    f7     d8                 ee   2a*    
                                                                      *|      |\<-C11\<-C12(**h-\>f4**)*  
                                                                      *|      |     74          2b*  
                                                                      *|     v*  
                                                                      *|\<-C9(o/f3,f3)*  
                                                                           *53*

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

*C1\<-C2\<-C3\<-C4\<-C5\<-C6\<-C7(o/f2,f2)\<-C8\<-C10(**o/m,m**)*  
*20    bc    82    89    39    f7     d8                 ee   2a*    
                                                                      *|      |\<-C11\<-C12(**h-\>f4,o/f4**)*  
                                                                      *|      |     74          2b*  
                                                                      *|     v*  
                                                                      *|\<-C9(o/f3,f3)*  
                                                                           *53*
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

	SEE: [https://www.atlassian.com/git/tutorials/cherry-pick](https://www.atlassian.com/git/tutorials/cherry-pick)

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

| \# All branches$ git push \--all origin	Enumerating objects: 12, done.	Counting objects: 100% (12/12), done.	Delta compression using up to 8 threads	Compressing objects: 100% (10/10), done.	Writing objects: 100% (10/10), 2.92 MiB | 41.01 MiB/s, done.	Total 10 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0\)	To https://github.com/jmorales111/lab1demo.git		   e1f412a..c35ebd8  main \-\> main |
| :---- |

\- In GitHub, click to your avatar icon (right upper corner) \-\> Profile

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

		   

C1\<-C2\<-C3\<-C4\<-C5\<-C6\<-C7(**o/f2,f2**)\<-C8\<-C10\<-C13 (**h-\>m,o/m**)  
20    bc    82    89    39    f7    d8                  ee     2a      d8  
                                      				|         |\<-C11\<-C12(**h-\>f4,o/f4**)  
                                      				|         |      74          2b  
                                      				|         v  
                                      				|\<-C9(**o/f3,f3**)  
                                          			    53

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
     
     
     
     
     
     
     
   

| $ cd Downloads/Git/laboratorios/lab1\# Displays the old URL$ git remote \-v\# Update the URL$ git remote set\-url origin https://github.com/jmorales111/git\_basics.git$ git remote \-v |
| :---- |

	*NOTES:* 

- *Collaborators: They’ll also need to update the remotes if they cloned using the old URL*  
- *CI/CD pipelines: Update any scripts, deployments configs, or integrations that reference the old repo name*  
- *Webhooks & API calls: Check if they use hardcoded URLs*


### **38\. Update the repository**

Copy some files and create the [README.md](http://README.md) in the local repository

| $ git checkout main$ git status \# Add [README.md](http://README.md) and other files in info directory$ git add \-A$ git status$ git commit \-m "README.md and other files in info directory added"$ git log \--graph \--decorate \--oneline \--all \--branches\# All branches$ git push \--all origin |
| :---- |

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

* ## [https://github.com/github/gitignore/tree/main](https://github.com/github/gitignore/tree/main)

* ## [https://iterm2.com](https://iterm2.com)

* ## [https://www.atlassian.com/git/tutorials/cherry-pick](https://www.atlassian.com/git/tutorials/cherry-pick)

* [https://learngitbranching.js.org](https://learngitbranching.js.org)  
* [https://www.gitkraken.com/learn/git/git-flow](https://www.gitkraken.com/learn/git/git-flow)  
* [https://www.gitkraken.com/blog/trunk-based-development](https://www.gitkraken.com/blog/trunk-based-development)  
* [https://medium.com/@yanminthwin/understanding-github-flow-and-git-flow-957bc6e12220](https://medium.com/@yanminthwin/understanding-github-flow-and-git-flow-957bc6e12220)




[image1]: <data:image/png;base64,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>

[image2]: <data:image/png;base64,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>

[image3]: <data:image/png;base64,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>
