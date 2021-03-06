### MySql 数据库常用的命令

### 一、关于用户的操作

| 命令 | 说明 | 补充说明 |
| :--- | :--- | :------- |


### 二、关于数据库

| 命令      | 说明                     | 代码案例                                |
| :-------- | :----------------------- | :-------------------------------------- |
| databases | 查看所有的数据库         | show databases                          |
| use       | 使用哪个数据库           | use 数据库名称                          |
| database  | 查看当前是哪个数据库     | select database()                       |
|           | 创建数据库               | create database 数据库名称 charset utf8 |
| drop      | 删除数据库               | drop database 数据库名称                |
| drop      | 删除数据库               | drop database 数据库名称 if exists      |
|           | 查看当前使用的那个数据库 | select database()                       |

### 三、关于表的基本操作

| 命令               | 说明                     | 代码案例                                                                                            |
| :----------------- | :----------------------- | :-------------------------------------------------------------------------------------------------- |
| create             | 创建表                   | create table 表名(列名 类型)                                                                        |
| drop               | 删除表                   | drop table 表名                                                                                     |
| comment            | 描述                     | create table 表名(列名 类型 comment "描述内容")                                                     |
| primary key        | 主键                     |                                                                                                     |
| auto_increment     | 自动增长                 | 要先设置主键                                                                                        |
| desc 表名          | 查看表结构               | desc 表名                                                                                           |
|                    | 查看表创建结构           | show create table 表名                                                                              |
|                    | 查看数据库下表           | show tables                                                                                         |
| rename             | 修改表名                 | alter table 名字 1 rename to 名字 2                                                                 |
| modify             | 修改列的属性             | alter table 表名 modify 列名 新类型                                                                 |
|                    | 修改列名与属性           | alter table 表名 change 旧列名称 新列名称 列属性                                                    |
|                    | 新增列                   | alter tabel 表名 add 列名 列属性(ALTER TABLE resource ADD COLUMN url VARCHAR(150) AFTER name)                                                                    |
|                    | 删除列                   | alter table 表名 drop 列名                                                                          |
| order by 列名 asc  | 升序查询                 | select \* from 表名 order by id asc                                                                 |
| order by 列名 desc | 降序查询                 | select \* from 表名 order by id desc                                                                |
| limit              | 分页查询                 | select \* from 表名 limit 开始位置,取几条数据                                                       |
| insert             | 插入数据                 | insert into 表名(列名 1，列名 2,...) values(值 1，值 2，值 3)                                       |
| insert             | 一次插入多条数据         | insert into 表名(列名 1，列名 2,...) values(值 1，值 2，值 3),(值 1，值 2，值 3),(值 1，值 2，值 3) |
| delete             | 删除数据                 | delete from 表 where 列名= 值                                                                       |
| update             | 修改数据                 | update 表名 set 列名=修改的值 where 条件                                                            |
|                    | 修改自动增长的游标       | alter table 表名 auto_increment = 游标值                                                            |
| 通过更改来删除     | 删除自动增长             | alter table 表名 change 旧列名 新列名 数据类型                                                      |
| 通过更改来添加     | 添加自动增长(要在主键上) | alter table 表名 change 旧列名 新列名 数据类型 auto_increment                                       |
| count              | 计数                     | select count(\*) as "数量" from 表名                                                                |
|                    | 删除主键                 | alter table 表名 drop primary key                                                                   |
|                    | 添加主键                 | alter table 表名 change 旧列 新列 类型 primary key                                                  |
|                    | 添加主键                 | alter table 表名 add primary key(列名 1，列名 2)                                                    |
| unique             | 添加唯一约束             | 创建表的时候直接在字段中添加 unique                                                                 |
|                    | 手动添加唯一约束         | alter table 表名 add unique (列名)                                                                  |
|                    | 手动删除唯一约束         | alter table 表名 drop index 列名                                                                    |
|                    | 删除外键约束             | alter table 表名 drop foreign key 约束名字                                                          |
|                    | 非空约束                 | not null                                                                                            |

### 四、表约束

- 1、主键约束
  - primary key 表示主键约束，一个表中只能有一个主键，但是一个主键可以是几个字段
  - 直接创建表的时候创建主键
  - 添加主键:`alter table 表名 add primary key(字段1，字段2)`
  - 删除主键:`alter table 表名 drop primary key`
- 2、唯一约束

  - `unique`表示唯一，一个表中可以有多个唯一的字段，仅仅是表示该字段不能重复
  - 直接创建表的时候在字段上加上`unique`
  - 添加唯一:`alter table 表名 change 字段名 新字段名 数据类型 unique`
  - 删除唯一:`alter table 表名 drop index 列名`

- 3、外键约束一般指的是物理外键:从表中的值只能是父表已经有的值

  - 创建方式一:`foreign key(id) references 父表(id)` 表示本表中的 id 列与父表的 id 列进行外键约束
  - 创建方式二:`constraint 约束的名字 foreign key(id) references 父表(id)` 表示定义了约束的名称
  - 删除外键约束:`alter table 表名 drop foreign key 外键名称`

- 4、非空约束

  - not null

- 5、检查约束
  - `enum`的使用:使用枚举类型,只能选择里面的一个值
  - `set`的使用:使用`set`可以选择里面多个值

### 五、常见的查询语句

- 1、普通的查询:`select 列名1,列名2,列名3... from 表名`
- 2、普通的查询:`select 列名1,列名2,列名3... from 表名\G`
- 3、根据条件查询:`select 列名1,列名2,列名3... from 表名 where 列名 条件`
  - 条件有:=,>,<
- 4、计算`count`:`select count(*) as 别名 from 表名 where 条件`
- 5、分组查询`group`:`select count(*) from 表名 group by 列名`
- 6、`having`是对分组后继续过滤:`select count(*) from 表名 group by 列名 having count(*) 条件5;`
- 7、分组后排序:`select count(*) from 表名 group by 列名 order by count(*) desc`
- 8、查询非空的:`select * from 表名 where 列名 is not null`
- 9、`trim`的使用:`select * from 表名 where 列名= trim(值)`
- 10、`between`查询区域范围:`select * from 表名 where 字段 between 条件1 and 条件2`
- 11、`in`的使用:`select * from 表名 where 字段 in (值1,值2);`

### 六、多表查询

- 1、左连接 [`表 A 查询...left join 表 B on 关联条件`]
- 2、右连接 [`表 A 查询...right join 表 B on 关联条件`]
- 3、内连接 [`表A查询...[inner] join 表B on 关联条件`]

> 总结:

- 1、如果 A 左连接 B 那么主动权在 A
- 2、如果 A 右连接 B 那么主动权在 B

---

- 1、创建一个员工表


    ```mysql
    create table emp(
    	id int primary key auto_increment comment "用户id",
    	name varchar(100) comment "用户名",
    	age int comment "用户名",
    	dept_id int comment "部门表id"
    );
    ```

- 2、创建一个部门表

  ```mysql
  create table dept(
      dept_id int comment "部门表id",
      dept_name varchar(100) comment "部门名称"
  );
  ```

- 3、插入数据

  ```mysql
  insert into emp(name,age,dept_id) values("张三",20,1),("李四",25,2),("王五",22,1),("马六",28,2),("钱二",30,3);
  insert into dept(dept_id,dept_name) values(1,"人事部"),(2,"技术部"),(3,"财务部");
  ```

- 4、多表查询

  ```mysql
  select * from emp left join dept on emp.dept_id = dept.dept_id;

  select * from emp right join dept on emp.dept_id=dept.dept_id;

  select * from emp inner join dept on emp.dept_id=dept.dept_id;

  select * from emp join dept on emp.dept_id=dept.dept_id;
  ```

### 七、子查询

> 重要一点,在`mysql`语句中通过`select`查询出来的也是一张表，所以可以继续进行查询等操作

- 1、一种的`where`型的子查询

  - `select 列名1,列名2... from 表名 where (select ...)`

    ```mysql
    # 可以直接这样写查询年龄大于20的
    select * from emp where (select age >20);

    #根据某一个人的年龄作为条件
    select * from emp where age > (select age from emp where id= 3)
    ```

- 2、一种是`from`的子查询

  - `select 列名1,列名2... from 表1 as 别名,(select 列名1,列名2 from 表2) as 别名 where 条件`
  - 使用`from`的子查询要使用别名,有下面两种方式指定别名

    - `select * from 表名 as 别名`
    - `select * from 表名 别名`

    ```mysql
    select * from emp as em,(select * from dept) as de where em.dept_id=de.dept_id;
    ```

### 八、`mysql`中的索引

- 1、普通索引
  - `create index 索引名 on 表名(列名)`
  - `alter table 表名 add index 索引名(列名)`
  - 直接创建表的时候`create table 表名(...index 索引名(列名))`
- 2、唯一索引
  - `create unique index 索引名 on 表名(列名)`
  - `alter table 表名 add unique index 索引名(列名)`
  - 直接在创建表的时候`create table 表名(...unique index 索引名(列名))`
- 3、全文索引
  - 注意`mysql`的引擎哟是`myisam`(`alter table 表名 engine myisam`)
  - `alter table 表名 add fulltext 索引名(列名)`
  - `create fulltext index 索引名 on 表名(列名)`
- 4、主键索引 `primary key`

> 查看索引

- 1、`show indexes from 表名`
- 2、`show keys from 表名`
- 3、`show index from 表名`

> 删除索引的方法

- 1、`alter table 表名 drop index 索引名称`
- 2、`drop index 索引名 on 表名`

### 九、关于事务的介绍

> 在进行多表操作的时候(比如先删除表中数据,然后再插入数据),如果不加上事务,可能会出现的问题是数据已经删除了,但是没有插入进去

- 1、创建一个账户表

  ```sql
  create table `account`(
      id int primary key auto_increment comment '主键id',
      name varchar(100) not null unique comment '账户名',
      balance decimal(10,2) not null default 0 comment '账号金额',
      create_time timestamp default current_timestamp comment '创建时间',
      update_time timestamp default current_timestamp on update current_timestamp comment '更新时间'
  ) engine innodb default charset=utf8mb4;
  ```

* 2、初始化数据

  ```sql
  insert into account(name, balance) values('张三', 100), ('李四', 100);
  select * from account;
  ```

* 3、普通的进行转账操作(正常情况下是不会出错误的,能保证总金额是 200 元)

  ```sql
  -- 对id=1的账号转出钱10元
  update account set balance = balance - 10 where id = 1;
  -- 对id=2的账号转进钱10元
  update account set balance = balance + 10 WHERE id = 2;
  ```

* 4、故意写错第二条`sql`语句(会出现钱转出去了,但是没转进去,总金额少了 10 元)

  ```sql
  -- 对id=1的账号转出钱10元
  update account set balance = balance - 10 where id = 1;
  -- 对id=2的账号转进钱10元
  update account set balance1 = balance + 10 WHERE id = 2;
  ```

* 5、给多步有关联的`sql`操作增加事务

  ```sql
  set autocommit = 0; -- 取消自动提交
  BEGIN;
  -- 对id=1的账号转出钱10元
  update account set balance = balance - 10 where id = 1; -- 提交一笔数据,但是在别的窗口中看不到id=1的用户balance金额减少了
  ROLLBACK; -- 表示回滚的意思
  -- 对id=2的账号转进钱10元
  update account set balance = balance + 10 WHERE id = 2;
  COMMIT; -- 对几条sql语句执行完后,在统一的commit,只有统一的commit后别的窗口才能看的数据的变动
  ```

* 6、下面是一段`eggjs`项目中使用事务的操作

  ```js
  async setUser({ roleId, userList }) {
      const { app } = this;
      // 开启事务
      const conn = await app.mysql.beginTransaction();
      try {
          // tslint:disable-next-line:array-bracket-spacing
          await conn.query('delete from role_user where role_id=?', [roleId]);
          for (const userId of userList) {
            await conn.insert('role_user', {
                role_id: roleId,
                user_id: userId,
            });
          }
          // 统一提交数据
          conn.commit();
      } catch (e) {
          // 如果有错误发生就回滚
          await conn.rollback();
          throw e;
      }
  }
  ```
