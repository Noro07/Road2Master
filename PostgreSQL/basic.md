# PostgreSQL

## 链接到数据插入数据并读取

```python
    conn = psycopg2.connect(database="", user="",
                            password="", host="", port="")
    cursor = conn.cursor()
    sql: str = ("INSERT INTO db.table"
                "(id)"
                "VALUES('001')")
    cursor.execute(sql)
    conn.commit()
    # delete
    cursor.execute("select * from db.table")
    rows = cursor.fetchall()
    print(rows)
    # delete end
    cursor.close()
    conn.close()
```

## 批量插入

使用extras的效率远比execute一句一句高很多

```python
import psycopg2
from psycopg2 import extras
value_collection = []
extras.execute_values(
            cursor, "INSERT INTO db.table (displayName) VALUES %s", value_collection)
```

## 插入数据中有单引号

单引号的数据切断了ddl
1.添加反斜杠
2.添加大写 `E`

```python

def add_backslach(word):
    return word.replace("'", "\\'")

name = "Tom's laptop"
sql: str = ("INSERT INTO db.table "
                    "(displayName) "
                    f"VALUES(E'{add_backslach(name)}') "
```

## 增量更新

在平常对数据库的操作中，我们经常会需要查看表中的某个字段是否存在来对数据库进行增加或更新操作
要求：如果 partner_terminal 表中的 terminal_id 字段不存在则添加数据，否则更新该条数据。

首先、设置唯一约束 unique
设置唯一约束，使该字段成为唯一 key
这里可以是两个 unique(a,b)

```ddl
alter table partner_terminal add constraint id_cons unique(terminal_id);
```

然后、对数据库进行添加或更新操作
根据唯一约束条件判断是否 inert 或 update

```ddl
INSERT INTO partner_terminal (
    id, partner_id, terminal_id, status,
    bind_time, create_time, update_time
)
VALUES (
    '6000', '1550', '5024', '0',
    now(), now(), now()
)
on CONFLICT(terminal_id)
do update
set
    status='2',
    update_time = now()
```
