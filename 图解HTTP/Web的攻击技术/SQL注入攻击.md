#### SQL 注入攻击

SQL注入攻击危害：

- 非法查看或篡改数据库的数据
- 规避认证
- 执行和数据库服务器业务管理的程序

攻击案例：

- 破坏SQL语句结构

利用--在SQL中表示注释，模糊查询条件

```java
SELECT * FROM bookTb1 WHERE author = '$q' and flag = 1
SELECT * FROM bookTb1 WHERE author = '上官野' --' and flag = 1
```



