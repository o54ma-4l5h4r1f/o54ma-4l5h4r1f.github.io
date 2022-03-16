---
sort : 13
--- 

# Git 

Typically, I prefer to setup a new github repository on the browser.
But if you already have a repo, and you want to clone it and make some editing on it, and push it back...follow these steps  

## Basic Configuration

```bash
cd Repo
git config --list
```

simply define your username and email regarding your github account.

```bash
git config --global user.name "<UserName>"

git config --global user.email "<EmailAddress>"
```
o54ma-4l5h4r1f
------ 

Git Large File Storage lets you store them on a remote server such as GitHub. Download and install git-lfs by placing it into your $PATH. You will then need to run the following command once per local repository:

```
git lfs install
```

Large files are selected by:

```
git lfs track '*.nc'
git lfs track '*.csv'

```
This will create a file named .gitattributes, and voilà! You can perform add and commit operations as normal. Then, you will first need to a) push the files to the LFS, then b) push the pointers to GitHub. Here are the commands:

```
git lfs push --all origin master    # master/main
git push -u origin master
```