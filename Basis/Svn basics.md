## SVN（SubVersion）概述
目的：协作开发、远程开发、版本回退（时间机器）
SCM-软件配置管理 对软件源代码进行管理和控制

- CVS: 元老级产品
- VSS: 入门级产品
- ClearCase: IBM公司提供技术支持
- SVN: 主流产品 CSV接班人

属于C、S结构软件（客户端与服务端）

获取软件
- [server-VisualSVN](http://www.visualsvn.com/)  
  安装过程选项
  + 第二步：具有可视化界面/只有DOS管理界面/添加SVN指令到系统环境变量中 
  + 8443端口 Backups是备份数据的存放目录  
- [client-Tortoisesvn](http://tortoisesvn.net/downloads)
  + 汉化包

SVN工作流程  
![svn工作流程.png](/images/image.png)  

SVN服务器端配置
1. 创建一个项目
  - 首先在SVN服务器创建一个公有目录作为项目目录
  - 在WebAPP目录下创建Shop文件夹 作为Shop(版本仓库 SVN中没有项目目录的概念 一个项目就是一个仓库)
  - 创建版本仓库 DOS环境基本语法：  
    `svnadmin create Shop 文件夹路径(有空格加双引号)`（Shop 仓库）  
    [conf db数据存储位置 hooks locks format版本仓库的层次结构 README.txt]
  - 进行服务器端监管  
    Apache— http://localhost:8080 访问htdocs目录  
    SVN— svn://localhost: 访问相关的数据仓库（如shop） 
    基本语法: `svnserve -d（后台运行 光标持续闪烁） -r（监管目录） D:/svn/WebApp/Shop（版本仓库路径）`  
    通过以上指令，此时`svn://localhost`或`ip地址`就可以直接指向Shop版本仓库
  - 权限控制
    默认情况下，SVN服务器不允许匿名用户上传文件到服务端的，所以必须更改项目的相关配置文件conf。  
    [authz授权文件 hooks-env.tmpl钩子的模板文件 passwd svnserver.conf核心配置文件]
    `svnserver.conf` --> `# anon-access = read` --> `anon-access = write` write可读可写
    
  2. 使用客户端软件连接SVN服务器（checkout检出）
  - 新建项目目录jingli
  - 在项目目录右键—>TortoiseSVN --> 版本库浏览器 --> 输入SVN服务器地址`svn://localhost`
  - svn://svn服务器地址 --> Shop目录（仓库） 该指向是由于监管操作 （检出至 `jingli目录` 生成`.svn目录`） 
  ![svn版本库浏览器.png](/images/svn版本库浏览器.png)  
  
  
    
    
    
    
    
