# MySQL作业

#  题目

作业详情：

- 数据库作业（命名为MySQL）





# 分析&答案



**图书表(book)**

- book_id(图书号) 
- author_id(作者号) 
- book_name(书名)
- pages(页数) 
- price(价格) 
- press(出版社)

> 分析：
>
> - 尽量不选择业务id作为主键，新建自增主键id；
> - 页数的范围不太可能超过65535，可选择SMALLINT类型
> - price要保证精确度，选择定点数DICIMAL
> - 其余字段选择INT和VARCHAR类型即可（公司建议尽量不要使用TEXT）



**奖项表(award)**

- book_id(图书号)
- author_id(作者号)
- cup_type(奖项类型金/银/铜)
- cup_time(获奖时间)

> 分析：
>
> - 尽量不选择业务id作为主键，新建自增主键id；
> - cup_type可选用TINYINT或ENUM类型，公司建议使用TINYINT而不是ENUM，但使用TINYINT需要做好COMMENT
> - 个人认为 cup_time 只需要取 YYYY-MM-DD 即可，无需关注 HH:MM:SS，所以使用 DATE 类型即可，占用字节更少，存储开销低。
> - 其余字段选择INT即可



**作者表(author)**

- author_id(作者号)
- author_name(作者名)
- content(作者简介)

> 分析：
>
> - 尽量不选择业务id作为主键，新建自增主键id；
> - author_name和content选用VARCHAR即可，但content要注意最大存储长度。







## Q1、设计表

根据上面给出的表字段信息，写出建表语句(我给出的字段内容、名称仅供参考，各位同学可以按照自己的设计建表)

> **考察点：**
>
> - 表是否加主键（若无主键，最高C）
> - 对存储引擎的掌握
> - 对字段定义的掌握，对字段类型的选择掌握
> - 对公司建表规范的掌握





## Q2：根据上面给出的表信息，结合以下信息合理设计索引，并写出创建索引的语句

1. 查询某作者出版了哪些图书
2. 查询某作者获得过哪些奖项，对应什么作品
3. 查询某作者某段时间内获得过哪些奖项



> **考察点：**
>
> - 对索引字段选择的掌握
> - 联表查询关联字段的字段是否创建索引，字段类型是否一致
> - 对DDL合并技巧的掌握





**三、完成以下SQL**

1. 查询姓王的作者有多少
2. 查询获奖作者总人数
3. 查询同时获得过金奖、银奖的作者姓名
4. 查询获得过金奖的图书有多少本，银奖的有多少本
5.  查询最近一年内获过奖的作者姓名



> **考察点：**
>
> - 对连接查询的掌握
> - 对简化语句、分拆语句的理解





**四、**

1. 如何查看表的结构信息？如何查看索引选择性？

2. 联合索引中的字段顺序应该如何设计？

3. 以下查询应如何创建索引？

   ```mysql
   select * from tb1 where name='zww' order by create_time desc limit 10;
   
   select * from tb1 where create_time between '2016-08-01 0:00:00' and '2016-08-31 23:59:59';
   ```

   

4. char(10)和 varchar(10)，varchar(100)有什么区别？简单描述一下什么场景下用哪个类型

5. 在utf8字符集和utf8mb4字符集下，varchar(50)分别能存储多少字符？创建索引时，字符串长度分别为多少，才能成功创建完整索引（而不是前缀索引）

6. 以下查询如何创建索引能够实现覆盖索引优化？(请给出具体SQL)

   ```java
   select invalid_time_flag from pushtoken_android_62 
       where uid = 'AC54E24E-FB73-3981-C4BC-CED8D69407F8' 
       and pid = '10010';
   
   select count(*) from pushtoken_android_62 
       where uid = 'AC54E24E-FB73-3981-C4BC-CED8D69407F8' 
       and pid = '10010'
   ```



> **考察点：**
>
> - 对索引设计的理解，对字段长度含义的理解，对字符集影响的理解，对覆盖索引概念的理解





**五、**

1. 公司mysql数据库采用那种字符集作为标准字符集？
   - 选项A latin1
   - 选项B utf8
   - 选项C gbk
   - 选项D utf8mb4
2. 在公司MySQL使用中如下哪些是不允许的？
   - 选项A 使用外键
   - 选项B 使用存储过程、触发器和自定义函数
   - 选项C 使用视图
   - 选项D 使用事件
3. 公司mysql数据库采用哪种存储引擎作为标准存储引擎？
   - 选项A MyISAM
   - 选项B InnoDB
   - 选项C NDB
   - 选项D MEMORY



> **考察点：**
>
> - 对开发规范的学习情况





# 答案



### 一、设计表

1. 

奖项表(award)中的 cup_type 字段的取值只有三个，可视为一种枚举类型。对于这种类型，我们可以用 tinyint 类型而非 int 类型来减少存储开销。tinyint 无符号数的取值范围为 0~255，有符号数的取值范围为 -128~127。

或者直接使用枚举类型 enum。



2. 



3. 

主键类型需要指定 unsigned



