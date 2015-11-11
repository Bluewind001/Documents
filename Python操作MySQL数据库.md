
## 1-1 课程简介
```flow
st=>start: 
ed=>end: 
op1=>operation: 客户端
op2=>operation: 业务逻辑层
op3=>operation: 数据访问层
sub=>subroutine: 数据库
st->op1->op2->op3->sub->ed
```

## 1-2 Python DB API 
数据库的连接对象：connection
数据库的交互对象：cursor
``` flow
st=>start: 开始
ed=>end: 结束
op1=>operation: 创建connection
op2=>operation: 获取cursor
op3=>operation: 执行查询
执行命令
获取数据
处理数据
op4=>operation: 关闭cursor
op5=>operation: 关闭connection

st->op1->op2->op3->op4->op5->ed
```

## 1-3 Python开发MySQL环境

## 2-1 数据库连接对象connection
连接对象：建立python数据端和数据库的网络连接。
创建方法：MySQLdb.Connect(参数)
参数名|类型|说明
---|---|----
host|字符串|MySQL服务器地址
port|数字|MySQL服务器端口号
user|字符串|用户名
passwd|字符串|密码
db|字符串|数据库名称
charset|字符串|连接编码


connection对象支持的方法：
方法名|说明
--|---
cursor()|使用该连接创建并返回游标
commit()|提交当前事务
rollback()|回滚当前事务
close()|关闭连接

## 2-2 游标对象cursor
支持的方法：
参数名|说明
--|--
execute(op[,args])|执行一个数据库的查询或命令
fetchone()|获取结果集的下一行
fetchmany(size)|获取结果集的下几行
fetchall()|获取结果集的剩下的所有行
rowcount|最近一次execute返回数据的行数或影响行数
close()|关闭游标对象

## 3-1 实例演示select数据


> Written with [StackEdit](https://stackedit.io/).