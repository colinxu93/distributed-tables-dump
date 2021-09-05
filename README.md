# DTD (Distributed Tables Dump) 
分布式表转储工具，能够将mysql分表数据导出到sqlite本地文件中。

# 名词解释
## 项目
包括一个具体的分布式表相关的配置（conf/项目.conf）、表内的数据（data/项目.db3）等。需要使用dtd进行初始化项目从而得到一个项目。

# 特性
1. 支持分库、分表数据合并
2. 支持自定义表前缀
3. 支持表后缀的形式：数值范围 [min, max]
4. 支持交互式操作：初始化项目（自动创建sqlite数据表）、数据转储（将项目的在远端的mysql数据转储到本地sqlite中）
5. 

# 安装
以下方式任选其一即可
## 下载二进制文件

## go get安装 - todo
```shell
go get github.com/colinxu93/dtd
```

## brew (mac)  - todo
```shell
brew install dtd
```
## yum (cents) - todo
```shell
yum install dtd
```

# 使用方法
## 初始化项目

### 初始化项目
```shell
./dtd init
```
#### 交互式模式
默认会按照交互式模式进行项目配置，依次需要配置：远端db分库个数、各个db分库的ip:port、用户名、密码

#### 命令行模式
支持按照命令行传参方式进行配置初始化项目

#### 命令行参数
```
-i --interact: 交互式模式, 默认, 有此参数后续参数均非必填
-c --cli: 命令行模式, 加上此参数后, 下面的参数都必填
-d --dsn: 远端db dsn, 多个通过英文分号";"分隔 
-n --name: 项目名
-p --table-prefix: 表前缀
-s --table-sufix-range: 表后缀范围, 以英文逗号分隔, 取闭区间[m,n],如：0,2047
```
#### 相关问题
1. 有的小朋友可能会问，初始化后想要修改配置怎么办？
修改conf/项目.toml即可

### 转储表数据
```shell
./dtd dump -s "select * from {table} where your condition"
```

#### 命令行参数
```
-s --sql: 输入需要查询转储数据的sql，其中 "{table}" 会被dtd解析替换成对应的具体分表名
```

## 转储数据使用
1. 转储数据为data目录下的：项目名.db3文件
2. 用户通过sqlite3命令行工具（windows、mac、centos等都自带这个工具）即可对项目产出的db3文件进行操作，支持sql查询、自定义格式导出等，具体参考：https://www.runoob.com/sqlite/sqlite-commands.html

# License
DTD is under the MIT License. See the LICENSE file for details.