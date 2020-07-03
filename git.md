## FATAL ##
```sh
git remote -v
git config --list
git status
git remote set-url origin '你的远端地址'
```

[https://blog.csdn.net/Leolu007/article/details/79129446](https://blog.csdn.net/Leolu007/article/details/79129446 "详情查看")

## 新的Git免密登录配置 ##
```sh
#查看是否有现有的公钥
cd ~/.ssh  No such file or directory
#进入根目录创建公钥
cd ~
ssh-keygen -t -rsa -c "xxx@qq.com"
#查看公钥
vi id_rsa.pub
#复制公钥到github账户，后进行本地配置
git -config --global user.name "yourname"
git -config --global user.email "xxx@qq.com"
#测试是否联通github仓库
ssh -T git@github.com
FINISHED！
```

## OTHERS ##
### 检查本机是否有ssh key设置 ###
```sh
$ cd \~/.ssh 或cd .ssh
#如果没有则提示： No such file or directory
#如果有则进入\~/.ssh路径下（ls查看当前路径文件，rm * 删除所有文件）
```

### 使用Git Bash生成新的ssh key。 ###
```sh
#保证当前路径在”~”下
$ cd ~  
#建议填写自己真实有效的邮箱地址
$ ssh-keygen -t rsa -C "xxxxxx@yy.com"  
Generating public/private rsa key pair.
#不填直接回车
Enter file in which to save the key (/c/Users/xxxx_000/.ssh/id_rsa):  
#输入密码（可以为空） 
Enter passphrase (empty for no passphrase):
#再次确认密码（可以为空）
Enter same passphrase again:   
#生成的密钥
Your identification has been saved in /c/Users/xxxx_000/.ssh/id_rsa.   
#生成的公钥
Your public key has been saved in /c/Users/xxxx_000/.ssh/id_rsa.pub.  
The key fingerprint is:
e3:51:33:xx:xx:xx:xx:xxx:61:28:83:e2:81 xxxxxx@yy.com
#*本机已完成ssh key设置，其存放路径为：c:/Users/xxxx_000/.ssh/下。
#注释：可生成ssh key自定义名称的密钥，默认id_rsa。
#生成ssh key的名称为githug_blog_keys，慎用容易出现其它异常。
$ ssh-keygen -t rsa -C "邮箱地址" -f ~/.ssh/githug_blog_keys 
```
### 添加ssh key到GItHub ###

 - 登录GitHub系统；点击右上角账号头像的“▼”→Settings→SSH kyes→Add SSH key。
 - 复制id_rsa.pub的公钥内容。 
     + 进入c:/Users/xxxx_000/.ssh/目录下，打开`id_rsa.pub`文件，全选复制公钥内容。
     + Title自定义，将公钥粘贴到GitHub中Add an SSH key的key输入框，最后`Add Key`

### 配置账户 ###
```sh
#设置用户名
$ git config --global user.name “your_username”  
#设置邮箱地址(建议用注册giuhub的邮箱)
$ git config --global user.email “your_registered_github_Email”  
```

### 测试ssh keys是否设置成功 ###
```sh
$ ssh -T git@github.com
The authenticity of host 'github.com (192.30.252.129)' can\'t be established.
RSA key fingerprint is 16:27:xx:xx:xx:xx:xx:4d:eb:df:a6:48.
#确认你是否继续联系，输入yes
Are you sure you want to continue connecting (yes/no)? yes 
Warning: Permanently added 'github.com,192.30.252.129' (RSA) to the list of known hosts.
#生成ssh kye是密码为空则无此项，若设置有密码则有此项且，输入生成ssh key时设置的密码即可。
Enter passphrase for key '/c/Users/xxxx_000/.ssh/id_rsa':  
#出现这句话，说明设置成功。
Hi xxx! You\'ve successfully authenticated, but GitHub does not provide shell access. 
```

##Githug PLAY
```
# ruby
apt install ruby
root@ali1:/home/ts# ruby --version
ruby 2.5.1p57 (2018-03-29 revision 63029) [x86_64-linux-gnu]
# gem
gem install githug
# githug 
root@ali1:/home/ts# githug
********************************************************************************
*                                    Githug                                    *
********************************************************************************
No githug directory found, do you wish to create one? [yn]  y
Welcome to Githug!

Name: init
Level: 1

root@ali1:/home/ts# cd git_hug/
root@ali1:/home/ts/git_hug# git init
Initialized empty Git repository in /home/ts/git_hug/.git/
root@ali1:/home/ts/git_hug# githug play

Name: config
Level: 2

root@ali1:/home/ts/git_hug# git config --local user.name aliyunUser
root@ali1:/home/ts/git_hug# git config --local user.email xxx@qq.com
root@ali1:/home/ts/git_hug# githug play

Name: add
Level: 3

root@ali1:/home/ts/git_hug# ls
README
root@ali1:/home/ts/git_hug# git add README
root@ali1:/home/ts/git_hug# githug play

Name: commit
Level: 4

root@ali1:/home/ts/git_hug# git add README
root@ali1:/home/ts/git_hug# git commit -m 'level4'
[master (root-commit) 5713613] level4
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README
root@ali1:/home/ts/git_hug# githug play

Name: clone
Level: 5

root@ali1:/home/ts/git_hug# git clone https://github.com/Gazler/cloneme
Cloning into 'cloneme'...
remote: Enumerating objects: 7, done.
remote: Total 7 (delta 0), reused 0 (delta 0), pack-reused 7
Unpacking objects: 100% (7/7), done.
root@ali1:/home/ts/git_hug# githug

Name: clone_to_folder
Level: 6

root@ali1:/home/ts/git_hug# git clone https://github.com/Gazler/cloneme my_cloned_repo
Cloning into 'my_cloned_repo'...
remote: Enumerating objects: 7, done.
remote: Total 7 (delta 0), reused 0 (delta 0), pack-reused 7
Unpacking objects: 100% (7/7), done.
root@ali1:/home/ts/git_hug# ls
my_cloned_repo
root@ali1:/home/ts/git_hug# githug play

Name: ignore
Level: 7

root@ali1:/home/ts/git_hug# ls
README.swp
root@ali1:/home/ts/git_hug# vim .gitignore
root@ali1:/home/ts/git_hug# githug play

Name: include
Level: 8

root@ali1:/home/ts/git_hug# ls
first.a  lib.a  second.a
root@ali1:/home/ts/git_hug# vim .gitignore
root@ali1:/home/ts/git_hug# githug play

Name: status
Level: 9

root@ali1:/home/ts/git_hug# ls
config.rb  database.yml  deploy.rb  Guardfile  README  setup.rb
root@ali1:/home/ts/git_hug# git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

    new file:   Guardfile
    new file:   README
    new file:   config.rb
    new file:   deploy.rb
    new file:   setup.rb

Untracked files:
  (use "git add <file>..." to include in what will be committed)

    database.yml

root@ali1:/home/ts/git_hug# git add database.yml
root@ali1:/home/ts/git_hug# git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

    new file:   Guardfile
    new file:   README
    new file:   config.rb
    new file:   database.yml
    new file:   deploy.rb
    new file:   setup.rb

root@ali1:/home/ts/git_hug# githug play

Name: number_of_files_committed
Level: 10

root@ali1:/home/ts/git_hug# ls
rubyfile1.rb  rubyfile4.rb  rubyfile5.rb  rubyfile6.rb  rubyfile7.rb
root@ali1:/home/ts/git_hug# git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

    new file:   rubyfile1.rb
    new file:   rubyfile4.rb
    new file:   rubyfile5.rb

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   rubyfile5.rb

Untracked files:
  (use "git add <file>..." to include in what will be committed)

    rubyfile6.rb
    rubyfile7.rb

root@ali1:/home/ts/git_hug# githug play

Name: rm
Level: 11

root@ali1:/home/ts/git_hug# ls
root@ali1:/home/ts/git_hug# git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

    new file:   deleteme.rb

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    deleted:    deleteme.rb

root@ali1:/home/ts/git_hug# git rm deleteme.rb
rm 'deleteme.rb'
root@ali1:/home/ts/git_hug# githug play

Name: rm_cached
Level: 12

root@ali1:/home/ts/git_hug# git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

    new file:   deleteme.rb

root@ali1:/home/ts/git_hug# git rm --cached  deleteme.rb
rm 'deleteme.rb'
root@ali1:/home/ts/git_hug# githug play

Name: stash
Level: 13

root@ali1:/home/ts/git_hug# ls
lyrics.txt
root@ali1:/home/ts/git_hug# git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

  modified:   lyrics.txt

no changes added to commit (use "git add" and/or "git commit -a")
root@ali1:/home/ts/git_hug# git stash
Saved working directory and index state WIP on master: 0206059 Add some lyrics
root@ali1:/home/ts/git_hug# git status
On branch master
nothing to commit, working tree clean
root@ali1:/home/ts/git_hug# githug

Name: rename
Level: 14


```
