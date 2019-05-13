# 1905-initial-operations

## overview

- log for creating initial environment of learning subjects

## logs

### 1. `git init sma19`

```bash
(base) g:\workspace>git init sma19
Initialized empty Git repository in g:/workspace/sma19/.git/

(base) g:\workspace>cd sma19

(base) g:\workspace\sma19>
(base) g:\workspace\sma19>echo # Smart SE 19a > README.md

(base) g:\workspace\sma19>gibo dump python node vim jekyll gitbook > .gitignore

(base) g:\workspace\sma19>powershell ls

    Directory: G:\workspace\sma19

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       13/05/2019     16:46           3070 .gitignore
-a----       13/05/2019     16:45             17 README.md


(base) g:\workspace\sma19>git add .
(base) g:\workspace\sma19>git status
On branch master
Initial commit
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   .gitignore
        new file:   README.md


(base) g:\workspace\sma19>git commit -m "initial commit"
[master (root-commit) e3cb420] initial commit
 2 files changed, 228 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 README.md

(base) g:\workspace\sma19>git remote add origin https://github.com/sakai-memoru/sma19.git

(base) g:\workspace\sma19>git config --list
core.symlinks=false
core.autocrlf=true
core.fscache=true
color.diff=auto
color.status=auto
color.branch=auto
color.interactive=true
help.format=html
http.sslcainfo=C:/Program Files/Git/mingw64/ssl/certs/ca-bundle.crt
diff.astextplain.textconv=astextplain
rebase.autosquash=true
credential.helper=manager
core.autocrlf=true
user.name=memoru
user.email=sakai.memoru@gmail.com
core.repositoryformatversion=0
core.filemode=false
core.bare=false
core.logallrefupdates=true
core.symlinks=false
core.ignorecase=true
remote.origin.url=https://github.com/sakai-memoru/sma19.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*

```

