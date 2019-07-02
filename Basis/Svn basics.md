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
![svn工作流程.png](/images/svn工作流程.png)  

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
  
## SVN基本使用
- SVN三大指令
  + Checkout 检出操作：  
    （Checkout只在第一次链接时操作一次，以后如果进行更新操作则使用Update（更新指令））  
    连接到SVN服务器端  更新服务端数据到本地
  + Commit 提交操作：  
    提交本地数据到服务器端
  + Update 更新操作：
- 图标集
  + 常规图标normal 当客户端文件与服务器端文件完全同步时 系统显示以上图标
  + 冲突图标conflictes 当客户端提交的文件与服务器端数据有冲突
  + 删除图标deleted
  + 增加图标added
  + 无版本控制图标non-versioned 当我们编写的文件没有添加到上传队列时
  + 修改图标modified
  + 只读图标readonly
  + 锁定图标locked 当服务器端数据已锁定 则客户端文件将自动显示锁定图标
  + 忽略图标ignore 客户端文件已忽略 不需要进行提交上传 `TortoiseSVN --> add to ignore list`
    
- 版本回退
  更新至版本 --> 根据日志回退 根据版本号回退  
    
  全递归：检出完整的目录树，包含所有的文件或子目录    
  直接子节点，包含文件夹：检出目录，包含其中的文件或子文件夹，但是不递归展开子文件夹  
  仅文件子节点：检出指定目录，包含所有文件，但是不检出任何子文件夹  
  仅此项：只检出目录。不包含其中的文件或子文件夹  
  工作副本：保持工作副本指定的深度。此选项不用于检出对话框，但它是其它所有含有深度配置对话框的默认配置  
  排除：对于已经创建好的工作副本，可以使用此选项来缩减文件夹的深度。这个选项只在更新至版本对话框中可用  

- 版本冲突（两个人同时修改某个文件）
  + 合理分配项目开发时间
  + 合理分配项目开发模块
  + 通过svn解决版本冲突问题
  
    更新服务器端数据到本地  
    [整合后的index.php文件 `.mine`自己修改后的index.php文件 `index.php.r6`初始更新时的index.php文件 `.r7`对方修改后的index.php文件]
    删除除index.php以外的其他三个文件
    
        <<<<<<< .mine
        本地修改集A
        =======
        版本库修改集B
        >>>>>>> 
    
    修改整合index.php冲突文件
    重新提交数据到SVN服务器端，即可解决版本冲突问题

- 配置多仓库与权限控制  
  通过监管总目录来达到监管所有仓库的目的 监管指令只能监管某一个文件夹  
  `svnserve -r -d 总目录`  
  `svn://localhost`或`ip地址`来访问总目录  
  子项目：`svn://localhost/子目录`

- 权限控制  
  如果要使用权限控制有一个前提：必须首先开启权限功能 
  在每一个仓库中都有一个conf文件夹，里面有三个文件  
  authz文件：授权文件  
  告诉哪些用户具有哪些权限  
  
  passwd文件：认证文件  
  标识当前svn系统中某个仓库具有哪些用户以及相应的密码  
    
  默认情况下，以上两个文件都是禁用，如果需要使用，首先开启以上两个文件  
  svnserve.conf 配置文件  
  
  开启步骤： 
  
      注释匿名用户的可读写权限`# anon-access = write`
      开启认证文件与授权文件 `27L password-db = passwd`和`36L authz-db = authz`
      编写认证文件定义相关用户名和密码  `passwd文件`  
      
  编写授权文件 `组名 = 列表名称`  
    ```
    [Shop:/]
    @admin = rw
    @users = rw
    # 匿名用户只有可读权限
    * = r
    ```
     
- SVN服务的配置与管理
 1. 配置自启动服务





