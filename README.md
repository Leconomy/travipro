
1:用github账号登陆Travis CI.

2:在右上角你的账户名点击进入 account，在Repositories tab页点击Sync now同步你的github项目，

3:选中项目将默认的off改变为on开启项目的持续集成。

4:在你项目的根目录建立一个.travis.yml文件，内容为：

language: node_js

node_js:  

     - 0.4  

     - 0.6

5: 提交code到github，打开tracivs ci界面等待其同步并运行你的build构建

6: 安装trais客户端 gem install travis

7: 登陆travis login --auto

8: 然后将刚刚生成的 id_rsa 复制到 .travis 文件夹，用命令行工具进行加密
	travis encrypt-file id_rsa --add
	这个时候会生成加密之后的秘钥文件 id_rsa.enc ，原来的文件 id_rsa 就可以删掉了

9: 为了让 git 默认连接 SSH 还要创建一个 ssh_config 文件。在 .travis 	
	文件夹下创建一个 ssh_config 文件

10: Host 远程服务器地址
    User 用户名
    StrictHostKeyChecking no
    IdentityFile ~/.ssh/id_rsa
    IdentitiesOnly yes

11: 完整的.travis.yml
	language: node_js
	node_js:
	- 7.7.1
	after_script:
	- scp -o StrictHostKeyChecking=no app.js root@www.zhoubo.xin:/home/www/yidengtest
	before_install:
	- openssl aes-256-cbc -K $encrypted_204d80cb93e1_key -iv $encrypted_204d80cb93e1_iv
	  -in .travis/id_rsa.enc -out id_rsa -d
	- mv id_rsa ~/.ssh -f
	- chmod 600 ~/.ssh/id_rsa
	# 配置 ssh
	- eval $(ssh-agent)
	- ssh-add ~/.ssh/id_rsa
	- cp .travis/ssh_config ~/.ssh/config
