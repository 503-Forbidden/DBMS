
```sql
create table employee (
    employee_name varchar2(50) primary key,
    street varchar2(100),
    city varchar2(50)
);
```

```sql
create table company (
    company_name varchar2(50) primary key,
    city varchar2(50)
);
```

```sql
create table works (
    employee_name varchar2(50) primary key,
    company_name varchar2(50),
    salary number(10,2),
    foreign key (employee_name) references employee(employee_name),
    foreign key (company_name) references company(company_name)
);
```

```sql
create table manages (
    employee_name varchar2(50) primary key,
    manager_name varchar2(50),
    foreign key (employee_name) references employee(employee_name)
);
```

```sql
create table department as select * from employee;
```

```sql
create table emp_backup as select * from employee where 1 = 0;
```

Add the column:

```sql
alter table employee add phone_number varchar2(15);
```

```sql
desc employee;
```

```sql
alter table company modify city varchar2(100);
```


```sql
alter table employee drop column phone_number;
```

```sql
alter table works rename column salary to monthly_salary;
```

```sql
insert into company values ('acme corp', 'pune');
```

```sql
insert into company values ('tech solutions', 'mumbai');
```

```sql
truncate table company;
```

```sql
alter table works modify monthly_salary decimal(10,2);
```
