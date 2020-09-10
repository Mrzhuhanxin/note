# 注意：安装zsh、docker、git工具需要开启翻墙
1、在用户根目录下创建app文件夹，将jdk、maven、postman、idea等压缩包放入然后逐个解压，删除压缩包
2、在/etc/profile文件中加入
```bash
export JAVA_HOME=/app/jdk1.8.0_201
export PATH=$JAVA_HOME/bin:$PATH
export MAVEN_HOME=/app/apache-maven-3.6.1
export PATH=$MAVEN_HOME/bin:$PATH
```
3、执行source /etc/profile
4、查看jdk和maven是否配置成功，执行java -version和mvn -version
5、安装zsh
```shell
# 首先更新系统包
sudo apt-get update
# 必须首先安装git
sudo apt-get install git
# 安装zsh
sudo apt-get install zsh
# 切换shell
chsh -s /bin/zsh
# 安装oh my zsh
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
或者
sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
# 配置oh my zsh
# 配置文件在.zshrc
切换主题为ys,修改为ZSH_THEME="gnzh"
# 新建自定主题、插件目录
mkdir -p ~/.zsh/plugins
在.zshrc文件中添加ZSH_CUSTOM=~/.zsh
# 添加插件
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.zsh/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions.git  ~/.zsh/plugins/zsh-autosuggestions
# 修改.zshrc
plugins=(git zsh-autosuggestions zsh-syntax-highlighting mvn)
# 添加别名文件.bash_aliases到当前用户的根目录
    alias ls='ls --color=auto'
    alias ll='ls -l --color=auto'
    alias atayun-aw-prod='ssh centos@52.221.213.70' 
    alias atayun-aw-dev='ssh ec2-user@52.220.156.222'   
    alias atayun-aw-justscoot-dev='ssh common@47.94.239.135'
    alias anywheel-package='mvn clean install -Dmaven.test.skip -P sgprod'
    alias anywheel-scp='scp target/exappgw-1.0.9.RELEASE.jar centos@52.221.213.70:~'
    alias mvnci='mvn clean install -Dmaven.test.skip'
    alias mvnrun='mvn spring-boot:run'
    alias atayun-prod='ssh -p 27744 root@144.34.244.233'  
    alias aliyun-free='ssh root@47.103.197.254'
    alias deepin-update='sudo apt-get update && sudo apt-get dist-upgrade -y && sudo apt autoremove'
    alias proxy='./client_linux_amd64 -s 39.106.35.253 -p 4901 -k eda2d1bb691f4034979a926d60ad3194'
    alias mvn-sonar='mvn sonar:sonar -Dsonar.host.url=https://sonar.atayun.com -Dsonar.login=45ec57ad9276e6be1aa93f92af9ac5ab22303b09'
    alias atayun-sxyd='ssh root@39.105.58.158'
    alias docker-stop='docker stop $(docker ps -q)'
    alias docker-rmi-none="docker images|grep none|awk '{print $3}'|xargs docker rmi"
# 在.zshrc文件中添加
setopt no_nomatch
if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi
```

6、生成ssh秘钥

ssh-keygen -t rsa

7、配置秘钥

```shell
# gitlab
Host git.atayun.com
User gitlab
IdentityFile /home/mrz/.ssh/id_rsa
IdentitiesOnly yes

# gitee
Host gitee.com
User gitee
IdentityFile /home/mrz/.ssh/id_rsa_gitee
IdentitiesOnly yes

```

8、安装git toolkit

- `sudo bash -c "$(curl -fsSL https://raw.githubusercontent.com/tonydeng/git-toolkit/master/installer.sh)"`

9、安装docker

- `sudo bash -c "$(curl -fsSL https://get.docker.com -o get-docker.sh)"`

10、加载镜像到docker容器中

- `docker load -i nginx-latest.tar.gz`
- `docker load -i mysql8.tar.gz`
- `docker load -i redis.tar.gz`
- `docker load -i docker-jdk8.tag.gz`
- `docker load -i mindoc.tar.gz`
