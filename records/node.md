# nodejs安装
## 1.下载nvm
	cd ~/git
	git clone https://github.com/creationix/nvm.git
## 2.执行nvm安装脚本
	source ~/git/nvm/nvm.sh
## 3.配置/etc/profile
在最后加上如下几行：

	export NVM_DIR="$HOME/git/nvm"
	[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
	[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
## 4.使用nvm安装node
	nvm list-remote
	nvm install v8.11.0
	nvm use v8.11.0