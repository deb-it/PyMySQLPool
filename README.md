## PyMySQLPool

A pymysql-based database connection pool, simple and lightweight.

Table of content

- [Features](https://github.com/zongzhenh/PyMySQLPool#features)
- [Requirements](https://github.com/zongzhenh/PyMySQLPool/blob/master/README.md#requirements)
- [Installation](https://github.com/zongzhenh/PyMySQLPool/blob/master/README.md#installation)
- [Example](https://github.com/zongzhenh/PyMySQLPool/blob/master/README.md#example)
- [Resources](https://github.com/zongzhenh/PyMySQLPool/blob/master/README.md#resources)
- [License](https://github.com/zongzhenh/PyMySQLPool/blob/master/README.md#license)

### Features

- Maintain a minimum number of connection pools by default.
- If number of unuse connections less than zero, dynamically add connections to pool until current number of inuse connections equal maximum of pool.
- Release the idle connections in regular until number of unuse connections equal minimum of pool.

### Requirements

- Python -- one of the following:
    - CPython : 2.7 and >= 3.4
    - PyPy : Latest version
- MySQL Server -- one of the following:
    - MySQL >= 5.5
    - MariaDB >= 5.5
- PyMySQL: >= 0.94

### Installation

Package is uploaded on [PyPI](https://github.com/zongzhenh/PyMySQLPool/blob/master/README.md#pymysqlpool)

You can install with pip

```
$ python3 -m pip install PyMySQLPool
```

### Example

Make use of a simple table (Example in [MySQL doc](https://dev.mysql.com/doc/refman/8.0/en/creating-tables.html))

```mysql
mysql> CREATE TABLE pet (name VARCHAR(20), owner VARCHAR(20),
    -> species VARCHAR(20), sex CHAR(1), birth DATE, death DATE);

mysql> INSERT INTO pet
    -> VALUES ('Puffball','Diane','hamster','f','1999-03-30',NULL);
```

```python
from pool import Pool


pool = Pool(host='YOUR_HOST', port='YOUR_PORT', user='YOUR_USER', password='YOUR_PASSWORD',
            db='YOUR_DB', min_size=10, max_size=90)
pool.init()

connection = pool.get_conn()
cur = connection.cursor()
cur.execute('SELECT * FROM `pet` WHERE `name`=%s', args=('Puffball', ))
print(cur.fetchone())

pool.release(connection)
```

This example will print:

```
('Puffball', 'Diane', 'hamster', 'f', datetime.date(1999, 3, 30), None)
```

That's all.

### Resources

- [PyMySQL Documenation](https://pymysql.readthedocs.io/en/latest/index.html)
- [MySQL Reference Manuals](https://dev.mysql.com/doc/refman/8.0/en/)

### License

PyMySQLPool is released under the MIT License. See LICENSE for more information.

# Contributing

Thank you for your interest in contribution of PyMySQLPool, your help and contribution is very valuable. 

You can submit issue and pull requests. Please submit an issue before submitting pull requests.
