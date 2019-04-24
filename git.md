## 新的Git免密登录配置 ##
> 查看是否有现有的公钥
> cd ~/.ssh  No such file or directory
> 进入根目录创建公钥
> cd ~
> ssh-keygen -t -rsa -c "xxx@qq.com"
> 查看公钥
> vi id_rsa.pub
> 复制公钥到github账户，后进行本地配置
> git -config --global user.name "yourname"
> git -config --global user.email "xxx@qq.com"
> 测试是否联通github仓库
> ssh -T git@github.com
> FINISHED！

