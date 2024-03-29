Databases
=========
# NoSQL
### Cassandra
Download & Installation 
References: 

Local Deployment: [DataStax Blog: getting started with Apache Cassandra](http://www.datastax.com/2012/01/getting-started-with-cassandra)

[datastax community edition](www.datastax.com/download)
<ol>
<li> Choose the Tarball option except for DataStax OpsCenter</li>
<li> Move files to intended directory and uncompress:</li>
</ol>

```
tar -xzf dsc-cassandra-1.2.2-bin.tar.gz
```
<ol start="4">
<li> Switch to the new Cassandra bin directory and start up Cassandra:</li>
</ol>
```
cd dsc-cassandra-1.2.2/bin
sudo ./cassandra
```
<ol start="5">
Connect to Cassandra Server (Using CQL utility cqlsh)

<li> Locate cqlsh: same bin directory as Cassandra executable</li>
</ol>
```
./cqlsh
```
<ol start="6">
<li> Create Cassandra keyspaces (database in RDBMS) </li>
keyspace: holds data objects, the level to specify options for a data partitioning and replication strategy
</ol>
```
cqlsh> create keyspace dev
... with replication = {'class': 'SimpleStrategy', 'replication_factor'}
```
<ol start="7">
<li> Create data objects<.li>
Cassandra is based on Google Bigtable, use column families/tables to store data
rows are like RDBMS; can have different columns for different rows
(create column families in the keyspace dev)
</ol>
```
cqlsh> use dev;
cqlsh:dev> create table emp (empid int primary key, 
... emp_first varchar, emp_last varchar, emp_dept varchar);
```
<ol start="8">
<li> Insert data</li>
</ol>
```
cqlsh:dev> insert into emp(empid, emp_first, emp_last, emp_dept)
... values (1, 'fred', 'smith', 'eng');
cqlsh:dev> update emp set emp_dept = 'fin' where empid = 1;
```
<ol start="9">
<li> Query data</li>
</ol>
```
cqlsh:dev> select * from emp;
```
cannot set where clause on non-primary key
have to create a secondary index on non-primary key column
```
cqlsh:dev> create index idx_dept on emp(emp_dept);
cqlsh:dev> select * from emp where emp_dept = 'fin';
```

* Cassandra Architecture Overview
Reference

[Introduction to Apache Cassandra white paper](http://www.datastax.com/wp-content/uploads/2012/08/WP-IntrotoCassandra.pdf)

* Cloud Deployment

[Google cloud Cassandra](https://cloud.google.com/solutions/cassandra/)

* Other Online Tutorials

[DataStax Free Training](https://academy.datastax.com/)

[What The Heck Are You Actually Using NoSQL For](http://highscalability.com/blog/2010/12/6/what-the-heck-are-you-actually-using-nosql-for.html)

[How to Install Java 7 JDK](http://brianoneill.blogspot.ca/2012/11/installing-jdk-7-on-mac-os-x.html)
