---
sort : 13
--- 

# Git 

Typically, I prefer to setup a new github repository on the browser.
But if you already have a repo, and you want to clone it and make some editing on it, and push it back...follow these steps  


```
git clone https://github.com/o54ma-4l5h4r1f/o54ma-4l5h4r1f.github.io.git

git config --global user.name "o54ma-4l5h4r1f"
git config --global user.email "o54ma4l5h4r1f@gmail.com"

git config --list
```

> if you are using VS-Code, it will make you login into your github accout and authorize it self. 



## Github CLI
> [Installation](https://github.com/cli/cli)

> [On Linux and BSD](https://github.com/cli/cli/blob/trunk/docs/install_linux.md)




```bash
$ gh auth login

? What account do you want to log into?
> GitHub.com
  GitHub Enterprise Server

? You are already logged into github.com. Do you want to re-authenticate? (y/N) y

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

After Authentication and making some editing
```bash
git add .
git commit -m "comment"
git push -u origin master  # master or main or any other branch
```



<br><br>


## GIT LFS

Git Large File Storage (LFS) replaces large files such as audio samples, videos, datasets, and graphics with text pointers inside Git, while storing the file contents on a remote server like GitHub.com or GitHub Enterprise.

```bash
git lfs install
```

Select the file types you'd like Git LFS to manage (or directly edit your .gitattributes)

```bash
git lfs track '*.nc'
git lfs track '*.csv'
...
```

Now make sure .gitattributes is tracked

```bash
git add .gitattributes
```

And voilà! nothing more to do

```bash
git add file.csv
git commit -m "Add large file"
git push -u origin master
```





git lfs push --all origin master    # master/main ?? 