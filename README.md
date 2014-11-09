Databases
=========
# NoSQL
### Cassandra
* Download & Installation 
References: 
Local Deployment
[DataStax Blog: getting started with Apache Cassandra](http://www.datastax.com/2012/01/getting-started-with-cassandra)
1. [datastax community edition](www.datastax.com/download)
2. Choose the Tarball option except for DataStax OpsCenter
3. Move files to intended directory and uncompress: 
```
tar -xzf dsc-cassandra-1.2.2-bin.tar.gz
```
4. Switch to the new Cassandra bin directory and start up Cassandra:
```
cd dsc-cassandra-1.2.2/bin
sudo ./cassandra
```
Connect to Cassandra Server (Using CQL utility cqlsh)
1. Locate cqlsh: same bin directory as Cassandra executable
2. 
```
./cqlsh
```
3. Create Cassandra keyspaces (database in RDBMS) 
keyspace: holds data objects, the level to specify options for a data partitioning and replication strategy
```
cqlsh> create keyspace dev
... with replication = {'class': 'SimpleStrategy', 'replication_factor'}
```
4. Create data objects
Cassandra is based on Google Bigtable, use column families/tables to store data
rows are like RDBMS; can have different columns for different rows
(create column families in the keyspace dev)
```
cqlsh> use dev;
cqlsh:dev> create table emp (empid int primary key, 
... emp_first varchar, emp_last varchar, emp_dept varchar);
```
5. Insert data
```
cqlsh:dev> insert into emp(empid, emp_first, emp_last, emp_dept)
... values (1, 'fred', 'smith', 'eng');
cqlsh:dev> update emp set emp_dept = 'fin' where empid = 1;
```
6. Query data
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
