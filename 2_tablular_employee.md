```sql
create table department (
    deptno number primary key,
    dname varchar2(50),
    location varchar2(50)
);
```
```sql
insert into department values (10, 'accounting', 'mumbai');
insert into department values (20, 'research', 'pune');
insert into department values (30, 'sales', 'nashik');
insert into department values (40, 'operations', 'nagpur');
```
```sql
create table employee (
    empno number primary key,
    ename varchar2(50) not null,
    job varchar2(50),
    mgr number,
    joined_date date,
    salary number(10,2),
    commission number(10,2),
    deptno number,
    address varchar2(50),
    foreign key (deptno) references department(deptno)
);
```
```sql
insert into employee values (1001, 'nilesh joshi', 'clerk', 1005, to_date('17-dec-95', 'dd-mon-yy'), 2800, 600, 20, 'nashik');
insert into employee values (1002, 'avinash pawar', 'salesman', 1003, to_date('20-feb-96', 'dd-mon-yy'), 5000, 1200, 30, 'nagpur');
insert into employee values (1003, 'amit kumar', 'manager', 1004, to_date('02-apr-86', 'dd-mon-yy'), 2000, null, 30, 'pune');
insert into employee values (1004, 'nitin kulkarni', 'president', null, to_date('19-apr-86', 'dd-mon-yy'), 50000, null, 10, 'mumbai');
insert into employee values (1005, 'niraj sharma', 'analyst', 1003, to_date('03-dec-98', 'dd-mon-yy'), 12000, null, 20, 'satara');
insert into employee values (1006, 'pushkar deshpande', 'salesman', 1003, to_date('01-sep-96', 'dd-mon-yy'), 6500, 1500, 30, 'pune');
insert into employee values (1007, 'sumit patil', 'manager', 1004, to_date('01-may-91', 'dd-mon-yy'), 25000, null, 20, 'mumbai');
insert into employee values (1008, 'ravi sawant', 'analyst', 1007, to_date('17-nov-95', 'dd-mon-yy'), 10000, null, null, 'amaravati');
```
```sql
select empno, ename, job, mgr, joined_date, salary, commission, deptno, address from employee;
```
```sql
select distinct job from employee;
```
```sql
update department set location = 'banglore' where deptno = 40;
```
```sql
update employee set ename = 'nikhil gosavi' where empno = 1003;
```
```sql
delete from employee where ename = 'pushkar deshpande';
```
```sql
select * from employee where job = 'manager' or job = 'analyst';
```
```sql
select * from employee where job in ('manager', 'analyst');
```
```sql
select ename, deptno from employee where deptno in (10, 20, 30, 40);
```
```sql
select ename, joined_date from employee where ename like 'a%';
```
```sql
select ename from employee where ename like '_i%';
```

```sql
select deptno, max(salary) from employee group by deptno having max(salary) > 5000;
```
