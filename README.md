
1:用github账号登陆Travis CI.

2:在右上角你的账户名点击进入 account，在Repositories tab页点击Sync now同步你的github项目，

3:选中项目将默认的off改变为on开启项目的持续集成。

4:在你项目的根目录建立一个.travis.yml文件，内容为：

language: node_js

node_js:  

     - 0.4  

     - 0.6

5: 提交code到github，打开tracivs ci界面等待其同步并运行你的build构建