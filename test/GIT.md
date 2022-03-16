---
sort : 13
--- 

# Git 

Typically, I prefer to setup a new github repository on the browser.
But if you already have a repo, and you want to clone it and make some editing on it, and push it back...follow these steps  

## Github CLI
> Installation <br>

https://github.com/cli/cli <br>
> on Linux and BSD <br>

https://github.com/cli/cli/blob/trunk/docs/install_linux.md


```bash
$ gh auth login

? What account do you want to log into?
> GitHub.com
  GitHub Enterprise Server

? You're already logged into github.com. Do you want to re-authenticate? (y/N) y

? What is your preferred protocol for Git operations?
> HTTPS
  SSH

? Authenticate Git with your GitHub credentials? No
? How would you like to authenticate GitHub CLI?    
> Login with a web browser
  Paste an authentication token

! First copy your one-time code: XXXX-XXXX
Press Enter to open github.com in your browser...

✓ Authentication complete.
- gh config set -h github.com git_protocol https
✓ Configured git protocol
✓ Logged in as o54ma-4l5h4r1f
```





----


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