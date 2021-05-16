### 文件权限  
chmod 755, 777, 644    
三个数字位置分别代表: 所有者 同组用户  公共用户  
而文件有三个操作权限 r(读)w(写)x(执行)，用每个权限用1和0区分是否有次权限，所以    
可读-可写-可执行： 111对应十进制 7 

### ssh 远程连连接
```
ssh root@ipaddress -p port 
#ipaddress和port可从供应商处获取，默认为22号端口
```

SSH连接的时候Host key verification failed.
vi ~/.ssh/known_hosts
删除对应ip的相关rsa信息

### 常用vim命令 
[vim常用命令](http://pizn.github.io/2012/03/03/vim-commonly-used-command.html)
esc 退出编辑， insert(i) 进入编辑模式  
:w	保存
:wq, :x	保存并关闭
:q	关闭（已保存）
:q!	强制关闭

h,j,k,l	 h表示往左，j表示往下，k表示往右，l表示往上
Ctrl+f	上一页
Ctrl+b	下一页
w, e, W, E	跳到单词的后面，小写包括标点
b, B	以单词为单位往前跳动光标，小写包含标点
O	开启新的一行
^	一行的开始
$	一行的结尾
gg	文档的第一行
[N]G	文档的第N行或者最后一行 


### 编辑host文件  
``` shell
sudo vi /etc/hosts
```