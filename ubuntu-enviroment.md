##
1. 安装shadowsocks
```bash
wget https://bootstrap.pypa.io/get-pip.py`
sudo python get-pip.py
sudo pip install shadowsocks
```

2. 安装chrome
`sudo wget http://www.linuxidc.com/files/repo/google-chrome.list -P /etc/apt/sources.list.d/`
`wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -`
`sudo apt update`
`sudo apt install google-chrome-stable`

3. 开启ssh
`sudo apt-get install openssh-server`
```bash
sudo vi /etc/ssh/sshd_config
找到：PermitRootLogin prohibit-password禁用
添加：PermitRootLogin yes
sudo service ssh restart
```

4. 配置shadowsocks
```json
{
        "server":"45.63.37.15",
        "server_port":443,
        "local_address":"127.0.0.1",
        "local_port":1080,
        "password":"Abc1234%",
        "method":"rc4-md5",
        "timeout":300,
        "fast_open":true,
        "workers":3
}

```

```
sudo vim /etc/init.d/shadowsocks
sudo chmod +x /etc/init.d/shadowsocks
sudo update-rc.d shadowsocks defaults  #添加开机启动
sudo service shadowsocks {start|reload|stop} 
```
```bash
#!/bin/sh

start(){
        ssserver -c /etc/shadowsocks.json -d start
}

stop(){
        ssserver -c /etc/shadowsocks.json -d stop
}

case "$1" in
start)
        start        
        ;;
stop)
        stop        
        ;;
reload)
        stop
        start        
        ;;
*)
        echo "Usage: $0 {start|reload|stop}"
        exit 1        
        ;;
esac
```

5. 设置pac代理
``bash
sudo pip install genpac
mkdir shadowsocks
cd shadowsocks
genpac --proxy="SOCKS5 127.0.0.1:1080" --gfwlist-proxy="SOCKS5 127.0.0.1:1080" -o autoproxy.pac --gfwlist-url="https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt"
```
将`/home/zhy/shadowsocks/autoproxy.pac` 放到url中即可

6. 配置vim
  - 安装vim插件管理器`git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim`
  - 编译youcompleteme 
    + `sudo apt-get install build-essential cmake`
    + `sudo apt-get install python-dev python3-dev`
    + `cd ~/.vim/bundle/YouCompleteMe`
    + `./install.py`

7. 安装powerline fonts
`git@github.com:powerline/fonts.git`


8. 安装zsh && on-my-zsh 
   + `sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`
   + 主题使用`agnoster`

9. 安装 oracle_jdk

