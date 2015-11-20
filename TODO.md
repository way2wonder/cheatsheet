##20150916

1. select的动态赋值
2. `load(object)` 方法为什么没有执行！！！     <font color=red>新增的时候不经过laod方法，修改的时候才经过load方法</font>





##20150917
#####TODO
1. 完善青贮窖类型字典
2. 所有form表单校验
3. 青贮窖的使用情况是否要提供部门信息

#####Need To  Improve
- hibernate
- javascript/jquery



##20150918
#####TODO
1. java的注解
2. TOAD的使用方法，回去研究下
#####Need To  Improve
1. 回去用maven搭建环境进行开发
2.  - [LeetCode网址](https://leetcode.com/)
    - [LeetCode答案](https://github.com/algorhythms/LeetCode)
    - [知乎上关于LeetCode的精彩回答](http://www.zhihu.com/question/35485418)
3. [LintCode](http://www.lintcode.com/zh-cn/problem/)  (没讨论)
4. [TopCoder](http://www.topcoder.com/)
5. [CodeForces](http://codeforces.com/)



##20150918
>青贮项目  

 1.  session 失效后的跳转页面要改成现在的
 


##20150921
1. 缓存的利用 ecache 等等
2. th的样式问题，换行后表格样式问题很严重




##20150922
1. 网易云课堂3阶魔方





###cheat sheet
1. tns配置

>set path=E:\app\Administrator\product\instantclient_10_2
>set ORACLE_HOME=E:\app\Administrator\product\instantclient_10_2
>set TNS_ADMIN=E:\app\Administrator\product\instantclient_10_2  
>set NLS_LANG=AMERICAN_AMERICA.AL32UTF8


2. Eclipse编辑js卡的解决方法

```xml
<buildSpec>
  <buildCommand>
   <name>org.eclipse.ui.externaltools.ExternalToolBuilder</name>
   <triggers>full,incremental,</triggers>
   <arguments>
    <dictionary>
     <key>LaunchConfigHandle</key>
    <font color="red"> <value>&lt;project&gt;/.externalToolBuilders/org.eclipse.wst.jsdt.core.javascriptValidator.launch</value></font>
    </dictionary>
   </arguments>
  </buildCommand>
  <buildCommand>
   <name>org.eclipse.jdt.core.javabuilder</name>
   <arguments>
   </arguments>
  </buildCommand>
  <buildCommand>
   <name>org.eclipse.wst.common.project.facet.core.builder</name>
   <arguments>
   </arguments>
  </buildCommand>
  <buildCommand>
   <name>org.eclipse.ui.externaltools.ExternalToolBuilder</name>
   <triggers>full,incremental,</triggers>
   <arguments>
    <dictionary>
     <key>LaunchConfigHandle</key>
     <font color="red"><value>&lt;project&gt;/.externalToolBuilders/org.eclipse.wst.validation.validationbuilder.launch</value></font>
    </dictionary>
   </arguments>
  </buildCommand>
 </buildSpec>
 <natures>
  <nature>org.eclipse.jem.workbench.JavaEMFNature</nature>
  <nature>org.eclipse.wst.common.modulecore.ModuleCoreNature</nature>
  <nature>org.eclipse.wst.common.project.facet.core.nature</nature>
  <nature>org.eclipse.jdt.core.javanature</nature>
  <nature>org.eclipse.wst.jsdt.core.jsNature</nature>
 </natures>
```


##20150923
1.  spring的权限框架


####全国青贮饲料平台TODO _List
1.玉米品种做成数据字典，具体的要和客户沟通下



##20150923
1. Log4j 框架的应用
2.


###cheat sheet
- 利用eclipse远程debug
    1. 开启tomcat的debug模式   
        + tomcat7已经设置了debug的参数，所以只需要以debug模式启动就行      
        + 运行方式： 在tomcat的bin目录创建一个debug.bat ,文件内容为：catalina.bat jpda start
        + 双击debug.bat启动tomcat
    2. eclipse远程debug
    右击工程  Debug as  > Debug Configuration > Remote Java Application  
    Host: 为tomcat所在服务器地址   
    port: 为tomcat设置的debug端口，默认为8000.  如果要设置成其他端口请自己在catalina.bat中修改
    3. 注意项
        + 注意服务器端的防火墙是否开启，如果开启了，请设置规则让debug端口通行






##20150925
Blogs  

1. [Axb的自我修养](http://2baxb.me/)
2. [Tim’s blog](http://timyang.net/)
3. [Coolshell](http://coolshell.cn/)
4. [花钱的年华：江南白衣的博客，后端相关，一线工程师的纯干货](http://calvin1978.blogcn.com/)
5. [开发者头条：每天扫一眼新鲜事](http://toutiao.io/)
6. [阮一峰的网络日志](http://www.ruanyifeng.com/blog/)
7. [玉伯](https://github.com/lifesinger/lifesinger.github.com/issues?labels=blog)
8. [云风的 BLOG](http://blog.codingnow.com/)
9. [justjavac(迷渡)](http://justjavac.com/)
10. [前端blog](http://www.libuchao.com/) 

WebSite

1.  [GITBOOK](https://www.gitbook.com)
2.  [GITHUB](https://github.com/)



##20150928

1.给UUR框架的DBUTIL增加 List<String> 之类的查询接口


2.框架的编辑用户信息有问题，保存邮箱的时候出错

3.看乔布斯毕业演讲


##20150929

1. GIT 入门与试用
2. [Nice Study WebSite](http://www.tutorialspoint.com/)

3. 字典的取值，取Value，以及缓存技术







##20151008

- s:iterator  循环遍历
```jsp
            <s:iterator value="varietyList" id="num">
                <s:iterator value="getSysCode('corn')">                  
                <s:if test="#num == id">  
                   <s:property  value="caption" />
                </s:if>
             </s:iterator> ,
                </s:iterator> 
```

- list 和map遍历结合

```jsp
    <s:iterator value="cornTypeList" id="num">
                <td width="100">&nbsp; <s:property  value="areaMap[#num]" /></td>               
     </s:iterator> 
```



##20151015

1.字符串 可以当场一个字符的数组var s = 'Hello, world!';   s[0]

字符串的常用方法：
toUpperCase        toLowerCase   indexOf   substring

indexOf

indexOf()会搜索指定字符串出现的位置：

var s = 'hello, world';
s.indexOf('world'); // 返回7
s.indexOf('World'); // 没有找到指定的子串，返回-1
substring

substring()返回指定索引区间的子串：

var s = 'hello, world'
s.substring(0, 5); // 从索引0开始到5（不包括5），返回'hello'
s.substring(7); // 从索引7开始到结束，返回'world'
2.  ARRAY

请注意，如果通过索引赋值时，索引超过了范围，同样会引起Array大小的变化：

var arr = [1, 2, 3];
arr[5] = 'x';
arr; // arr变为[1, 2, 3, undefined, undefined, 'x']




openOffice  启动
soffice -headless -accept="socket,host=127.0.0.1,port=8100;urp;" -nofirststartwizard 

安装完openoffice后

1.安装服务

cd C:\Program Files (x86)\OpenOffice 4\program

执行

soffice -headless -accept="socket,host=127.0.0.1,port=8100;urp;" -nofirststartwizard

2.查看是否安装成功

    2.1查看端口对应的pid

    netstat -ano|findstr "8100"

    2.2查看pid对应的服务程序名

    tasklist|findstr "ipd值"




###20151016

1. 工作流程--Activiti


###20151018
#####
1. vundle 插件管理vim插件。
2. markdown插件安装
3. git的学习，vim的学习



###20151023
1.  设计模式-静态工厂之服务提供者框架
2.  markdown 语法-区块引用

>11111111123  
>12321312  
>>12312  
>>312    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   <font  style="color:red">嵌套的区块引用下面必须有换行才行</font>
> 
>3123  
>123123


> ## 这是一个标题。
> 
> 1.   这是第一行列表项。
> 2.   这是第二行列表项。
> 
> 给出一些例子代码：
> 
>     return shell_exec("echo $input | $markdown_script"); 
>     


3. memcached      redis 比较



###20151027
######first:use jekyll 搭建个人blog
1. Linux基础
2. 数据结构与算法
3. sublime text/vim
4. dia
5. mysql
6. gitbook
7. html/css  js/jquery
8. apache shiro  (权限框架)
9. log4j
10. [Awesome-developer](http://developer.phodal.com/)



###20151028
1. IE 8下，浏览器会认为 [1,2,3,]的长度为4，即1，2，3，和undefined四个元素



###20151030
[Java学习的TOP20网站](http://www.simplilearn.com/resources-to-learn-java-programming-article)



###20151031
1. jsp 中格式化输出时间
  <fmt:formatDate value="${createDate}" pattern="yyyy年MM月dd日" />
2. s:iterator
   遍历的时候  
   ```jsp
      <s:iterator value="distributeSampleList" status="stat" id="target">  
      在s标签中用  name="distributeSampleList[%{#stat.index}].samplenum"  
      在原始标签中用 name="distributeSampleList[${stat.index}].checkdate"  
      </s:iterator>  
   ```

3.
`c:when 和c:otherwise 必须在  c:choose标签里`




###20151112

1. 待功能完善后将区域选择改成选择树
2. 
