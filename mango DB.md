参考文档：https://www.jianshu.com/p/fd7b422d5f93



MongoDB 是一个基于分布式文件存储的数据库。由 C++ 语言编写。旨在为 WEB 应用提供可扩展的高性能数据存储解决方案。

MongoDB 是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能最丰富，最像关系数据库的。

> **关系数据库：**指采用了关系模型来组织数据的数据库。关系模型指的就是二维表格模型，而一个关系型数据库就是由二维表及其之间的联系所组成的一个数据组织。
>
> **关系模型中常用的概念：**
>  关系：一张二维表，每个关系都具有一个关系名，也就是表名
>  元组：二维表中的一行，在数据库中被称为记录
>  属性：二维表中的一列，在数据库中被称为字段
>  域：属性的取值范围，也就是数据库中某一列的取值限制
>  关键字：一组可以唯一标识元组的属性，数据库中常称为主键，由一个或多个列组成
>  关系模式：指对关系的描述。其格式为：关系名(属性1，属性2， ... ... ，属性N)，在数据库中成为表结构
>
> ##### 当今十大主流的关系型数据库
>
> Oracle，Microsoft SQL Server，MySQL，PostgreSQL，DB2，Microsoft Access， SQLite，Teradata，MariaDB(MySQL的一个分支)，SAP
>
> 
>
> **非关系数据库：**指非关系型的，分布式的，且一般不保证遵循ACID原则的数据存储系统。
>
> ​	ACID原则是数据库事务正常执行的四个，分别指原子性、一致性、独立性及持久性。

# 1、下载

下载地址：<https://www.mongodb.com/download-center/community>

# 2、安装：

安装过程中可选择（custom）自定义路径

# 3、配置

如安装地址为：D:\Program Files\MongoDB\Server\4.0

（1）在D:\Program Files\MongoDB目录下创建一个文件夹（data）

![img](F:/%E6%9C%89%E9%81%93%E4%BA%91%E7%AC%94%E8%AE%B0/qq7CDC5A112BCA7A4C79CCA645C06DF674/e3c0ecf9a08c4ef289955700f9594c96/43c09e2475994803b4f2fa178ca14e31.jpg)

（2）在D:\Program Files\MongoDB\data目录下创建两个文件夹（db、log）

![img](file:///F:/%E6%9C%89%E9%81%93%E4%BA%91%E7%AC%94%E8%AE%B0/qq7CDC5A112BCA7A4C79CCA645C06DF674/f5d1edb60e424e9590cbf56ec66b8b86/1b460aeb753f44889b2db71480663716.jpg)

![img](file:///F:/%E6%9C%89%E9%81%93%E4%BA%91%E7%AC%94%E8%AE%B0/qq7CDC5A112BCA7A4C79CCA645C06DF674/24fc5cb0e85642f2a2d573a2ada51e7a/bff896b53d0f41408b6baa247ea4678e.jpg)

（3）在D:\Program Files\MongoDB\data\log目录下创建一个名为（mongodb.log）的文件

# 4、启动

进入D:\Program Files\MongoDB\Server\4.0\bin目录

输入mongod -dbpath "D:\Program Files\MongoDB\data\db"

![img](F:/%E6%9C%89%E9%81%93%E4%BA%91%E7%AC%94%E8%AE%B0/qq7CDC5A112BCA7A4C79CCA645C06DF674/fc9363262216455c8db22439c76b2b30/0e113ad6afbd462ca2b4f3448d4a7384.jpg)

![img](file:///F:/%E6%9C%89%E9%81%93%E4%BA%91%E7%AC%94%E8%AE%B0/qq7CDC5A112BCA7A4C79CCA645C06DF674/1875529ffe514851810e294150887112/633dda2b285d4bcd8b7156ba162f05de.jpg)

如出现如上图所示结果，说明启动成功，端口号为27017

# 5、另一种检验是否启动成功的方法

在浏览器中输入<http://localhost:27017/>

如出现如下提示，说明启动成功

It looks like you are trying to access MongoDB over HTTP on the native driver port.