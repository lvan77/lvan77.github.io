
 MarkDown主要分为：**标题，段落，区块引用，代码区块，腔调，列表，分割线，链接，图片，反斜杠```\```,符号
[markdown 语法参考](https://xianbai.me/learn-md/article/about/readme.html)

#### 转义字符
```
\ ` * _ {} 
[] () # + - 
. ! 
上面都是 MarkDown 用到的字符 ，"{}" 大括号目前未用到不知道用途
```  

#### 换行
``` <br/> ```


#### 标题：  
```
 一级标题
 =====
 二级标题
 -----
 或者
 #一级标题  
 ##二级标题  
 ###三级标题  
 ####四级标题  
 #####五级标题  
 ######六级标题  
 支持1-6级标题  
```
效果：   

一级标题
====
二级标题
----
# 一级标题  
## 二级标题  
### 三级标题  
#### 四级标题  
##### 五级标题  
###### 六级标题  

####段落:
 段落前后都要有空行（没有文字内容），  
 段内强制换行**_两个以上空格加回车(引用中换行省略回车)_**  
####区块引用
在段落的每行或者第一行使用```>```，还能嵌套使用   
```
>区块引用
>>嵌套引用
```

效果:  
>区块引用
>>嵌套引用  

####粗体，斜体
```
*这是斜体*
_这也是斜体_
**这是粗体**
***这是粗体+斜体***
注意要是再问吧中有"*"或者"_" 前面加 \ 转意
```

#### 删除线
```
~~删除线~~
```
~~删除线效果~~


#### 超链接
格式为: ```语法: [link text](url 'title') ```  
1. [普通链接百度](http://www.baidu.com '百度')  
```语法: [普通链接百度](http://www.baidu.com '百度') " "和'' 都可以，不用也可以 ```  
2. 自动链接 <http://www.baidu.com> 
```语法: <http://www.baidu.com>```  
3. [本地文件链接 sublimeText3配置.md](./sublimeText3配置.md) 
   ```语法: [本地文件链接 sublimeText3配置.md](./sublimeText3配置.md) ``` <br/> 

**图片和超链接的格式一样不过前面多一个!**  <br/> 
   即```语法: ![link text](url 'title') ```<br/> 

####分割线

三个或更多的```*```,```-,```,```_``` 中间也可以有空格
* * *
-----
___

####列表
```
* ,+ ,- ,都可以作为无序列表的标记（后面要加空格）
```
* 无序列表
+ 无序列表
- 无序列表
```
数字+"." 有序列表，数组不影响列表顺序，但是推荐按自然顺序（1.2.3.）编写，同样注意"."后面要有空格
```
1. 有序列表
2. 有序列表
3. 有序列表
```
嵌套列表
1. 第一层
    + 1-1
    + 1-2
2. 随意嵌套
    1. 2-1
    2. 2-2
```
1. 第一层
    + 1-1
    + 1-2
2. 随意嵌套
    1. 2-1
    2. 2-2
####表格
```
| 分割不同的单元格，-分割表头和其他行
    name | age 
    ---- | ----
    小明  | 11
    小王  | 12
```

name  | age
----  | ----
小明   | 11
小王   | 12
小哥   | 14

#### Task List
```
- [ ] 任务1
- [x] 任务2
    - [x] 任务2-1
    - [x] 任务2-2

- [ ] 任务一 未做任务 `- + 空格 + [ ]`
- [x] 任务二 已做任务 `- + 空格 + [x]`
```

- [ ] 任务一  
- [ ] 
- [x] 为毛不是想要的效果😂

{
什么用途？
}

## 常用插件 
插件安装方法 <br/>
1. 快捷键 ```ctrl + shift + P ``` 
2. 找到或输入 ```Package Control: Install Package``` 后回车  
3. 输入要安装的插件名字等待安装  

####  package control 被墙解决方案 
手动安装 package control 然后 更改配置 <br/>
1. git 下载 packageControl<https://github.com/lvan77/package_control> zip 包
2. 解压 重命名 *Package Control* 然后拷贝到 sublime packages目录下 Perferences->browsePackages 
3. 更改 packageControl userSetting ![添加配置](./imageSource/sublime3PackageControlSetting.png)
``` json
 ## 根据上面操作追加下面配置到文件中保存
    "channels":
    [
        "http://cst.stu.126.net/u/json/cms/channel_v3.json",
    ]
```

4. 常用插件  MarkdownEditing, MarkdownPreview, MarkdownLivePreview, LiveReload<br/>
MarkdownPreview 无法打开浏览器情况找到 Perferences ->PackageSetting -> MarkdownPreview ->Setting User 修改 <br/> 
``` json 
## user 里面没有内容的情况 拷贝 defult 里面的内容到user下
 "browser": "/Applications/Google Chrome.app",
```  

##  sublime text  使用  
- 保留上次打开文件  
``` json 
##  Perferences ->Setting 添加下面配置
    "hot_exit": true,
```




