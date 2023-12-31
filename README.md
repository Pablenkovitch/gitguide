﻿# The ultimate git guide for old dudes

## 1. Your first move
Install Git for your OS.
Check installation.

```
git version
```

## 2. Set up .gitconfig
From anywhere:

```
git config --global user.name "put_your_name_here"
```

```
git config --global user.email "put_your_email_here"
```

To check changes

```
git config --list
```

or

```
cat ~/.gitconfig 
```

## 3. Initialize your local repository
**Go to project catalog**

```
mkdir my_project_name
cd my_project_name
git init
``` 

Check this action by:

```
git status
```
 
## 4. Create what you need
Make some stuff **in project catalog**.

## 5. Add those files to your repo
To do this, go to the project catalog 

```
git add --all
``` 

or command to add current catalog:

```
git add .
``` 

Command to add specific file:

```
git add file_name
```
 
After changing something in files you have to 

```
git add
```
 
again

## 6. Committing changes 
Only after this command you save the changes 

```
git commit -m 'short description of change'
```

## 7. Checking
If you want to check the history of commits, use

```
git log
```

## 8. Create remote repo
VIA [GitHub](https://www.github.com "remote repo")

Than create my_project_name repo

After this step we will our connect our local repo to remote repo on GitHub.

But first of all we are going to make SSH-keys

## 9. SSH keys
You don't have to do this, but linking you local pero to remote repo VIA SSH will make your life easier.
Word.

### 9.1 Check if SSH_keys already exists

```
ls -la .ssh/ 
```

Delete if there are any you have not created.

### 9.2 Generate new pair of SSH-keys

``` 
ssh-keygen -t ed25519 -C "email linked to your GitHub"
```

or use another algorithm if you see an error message:

```
ssh-keygen -t rsa -b 4096 -C "email linked to your GitHub"
```

### 9.3 Choose place to store your keys
After this you will see a pair of files in chosen directory.

And you will be asked about creating code phrase. 
This can be skipped. Otherwise you will have to enter this phrase with every commit.

Then check keys:

```
ls -lah ~/.ssh
```

Two files will appear. One of them is .pub. It means public.

Other one is private. **No one should see it!**

### 9.4 Linking SSH-key with GitHub
Copy the internals of .pub file into buffer

```
pbcopy < ~/.ssh/id_rsa.pub
```

or

```
pbcopy < ~/.ssh/id_ed25519.pub
```

or

```
cat ~/.ssh/id_ed25519.pub
```

On Windows use 'clip' instead of 'pbcopy'
And copy output using alt+shift+c
Then go to **Settings** in GitHub's account.
Click "SSH and GPG keys". Then click "New SSH key".

In "Title" field spell key's name. "Personal key" for example.

"Key type" field must be "Authentication Key".

Into field "Key" paste your **public key** from buffer.

Press "Add SSH key".

### 9.4 Checking correctness.

```
ssh -T git@github.com
```
 
If this is your **first time**, you'll see

```bash
The authenticity of host 'github.com (140.82.121.4)' can't be established. ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU. This key is not known by any other names. Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Enter "Yes".

## 10. Linking our local repo with our remote repo.
Go to your remote repo's page on GitHub. Choose type "SSH". And copy an URL.

From **your local repo folder** 

```
git remote add origin git@github.com:%account_name%/project_name.git
```

In this command you give two parameters: remote repo's name and it's URL.

Meaning: "origin" - name, "git@github.com:%account_name%/project_name.git" - URL you copied.

Check link between two repos:

```
git remote -v
``` 

## 11. Push, baby, push.
It's time to deliver local file to remote repo.

In your **first time** do it like this:

```
git push -u origin main
```

After first time this would be enough:

```
git push
``` 

## 12. Useful info.
### 12.1 HEAD and use of git log 

```
git log
```

You will see 'HEAD -> master'. 
**HEAD** - is file, that points to the **last commit**
There is a pointer to refs/heads/master inside of 'HEAD'.

```
cat refs/heads/master
```

You will see a hash. Exactly like from:

```
git log
```

To make log short use:

```
git log --oneline
```

### 12.2 File life cycle in Git.
There are several stages in file life...Here they are:
1. Untracked.
2. Tracked.
3. Staged.
4. Modified.

```mermaid
graph LR;
  touch_file_name--"git status"-->untracked;
  untracked--"git add"-->staged;
  staged  -- "git commit"--> tracked/comitted;

```

```mermaid
graph LR;
  touch_file_name--"git status"-->untracked;
  untracked-->"git add"-->tracked/staged;
  staged-->"git commit -m meaningful message"-->tracked/comitted;
  tracked-->some changes--> modified;

```

## 13. Committing
Best practice is to commit with short and meaningful messages between 30 and 72 symbols.

Examples:

```
git commit -m "Add info about commits"
```

```
git commit -m "LGS-239: fix typos in line #496"
```

LGS-239 - project or task name.

### git commit -m '<type>:<message>'
Two possible types:
1. feat if feature was add
2. fix if something was fixed

```
git commit -m 'feat: add sum counter'
```

```
git commit -m 'fix: stack overflow'
``

