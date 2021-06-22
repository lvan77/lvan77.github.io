## rabbitmq 使用  

### Mac 下安装  
```shell 
brew update

brew install rabbitmq

```  

安装目录 
/usr/local/Cellar/rabbitmq/3.8.16 

配置环境变量  
```shell
vim ~/.bash_profile

// 加入环境配置
export RABBIT_HOME=/usr/local/Cellar/rabbitmq/3.8.16
export PATH=$PATH:$RABBIT_HOME/sbin

// 立即生效
source ~/.bash_profile

```

### 启动  





```shell
	// 后台启动
  rabbitmq-server -detached  
	// 查看状态
  rabbitmqctl status 
	// 访问可视化监控插件的界面
  	// 浏览器内输入 http://localhost:15672,默认的用户名密码都是guest,登录后可以在Admin那一列菜单内添加自己的用户
  	// 关闭
  rabbitmqctl stop

```
  