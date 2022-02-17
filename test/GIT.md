---
sort : 13
--- 

# Git 

## Basic Configuration

```bash
git config --global user.name "<UserName>"
```

```bash 
git config --global user.email "<EmailAddress>"
```

```bash
git config --list

user.name=o54ma-4l5h4r1f
user.email=o54ma4l5h4r1f@gmail.com

remote.origin.url=https://github.com/o54ma-4l5h4r1f/repo.git

```


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