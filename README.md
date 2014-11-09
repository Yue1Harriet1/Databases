Databases
=========
# NoSQL
### Cassandra
* Download & Installation 
References: 

Local Deployment

[DataStax Blog: getting started with Apache Cassandra](http://www.datastax.com/2012/01/getting-started-with-cassandra)
<ol>
<li> [datastax community edition](www.datastax.com/download)</li>
<li> Choose the Tarball option except for DataStax OpsCenter</li>
<li> Move files to intended directory and uncompress:</li>
```
tar -xzf dsc-cassandra-1.2.2-bin.tar.gz
```
<li> Switch to the new Cassandra bin directory and start up Cassandra:</li>
```
cd dsc-cassandra-1.2.2/bin
sudo ./cassandra
```
</ol>
Connect to Cassandra Server (Using CQL utility cqlsh)
<ol>
<li> Locate cqlsh: same bin directory as Cassandra executable</li>
```
./cqlsh
```
<li> Create Cassandra keyspaces (database in RDBMS) </li>
keyspace: holds data objects, the level to specify options for a data partitioning and replication strategy
```
cqlsh> create keyspace dev
... with replication = {'class': 'SimpleStrategy', 'replication_factor'}
```
<li> Create data objects<.li>
Cassandra is based on Google Bigtable, use column families/tables to store data
rows are like RDBMS; can have different columns for different rows
(create column families in the keyspace dev)
```
cqlsh> use dev;
cqlsh:dev> create table emp (empid int primary key, 
... emp_first varchar, emp_last varchar, emp_dept varchar);
```
<li> Insert data</li>
```
cqlsh:dev> insert into emp(empid, emp_first, emp_last, emp_dept)
... values (1, 'fred', 'smith', 'eng');
cqlsh:dev> update emp set emp_dept = 'fin' where empid = 1;
```
<li> Query data</li>
```
cqlsh:dev> select * from emp;
```
cannot set where clause on non-primary key
have to create a secondary index on non-primary key column
```
cqlsh:dev> create index idx_dept on emp(emp_dept);
cqlsh:dev> select * from emp where emp_dept = 'fin';
```
</ol>
* Cassandra Architecture Overview
Reference

[Introduction to Apache Cassandra white paper](http://www.datastax.com/wp-content/uploads/2012/08/WP-IntrotoCassandra.pdf)

* Cloud Deployment
* 
[Google cloud Cassandra](https://cloud.google.com/solutions/cassandra/)

* Other Online Tutorials

[DataStax Free Training](https://academy.datastax.com/)
[What The Heck Are You Actually Using NoSQL For](http://highscalability.com/blog/2010/12/6/what-the-heck-are-you-actually-using-nosql-for.html)
