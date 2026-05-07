```
create table stud_marks (
    roll number primary key,
    name varchar2(50),
    total_marks number
);
```
```
create table result (
    roll number,
    name varchar2(50),
    class varchar2(50)
);
```
```
insert into stud_marks values (101, 'amit', 1050); 
insert into stud_marks values (102, 'neha', 950); 
insert into stud_marks values (103, 'rahul', 850);  
insert into stud_marks values (104, 'pooja', 700);  
```
```
commit;
```
```
create or replace procedure proc_grade (p_roll in number) is
    v_name varchar2(50);
    v_marks number;
    v_class varchar2(50);
begin
    select name, total_marks into v_name, v_marks 
    from stud_marks 
    where roll = p_roll;

    if v_marks between 990 and 1500 then
        v_class := 'Distinction';
    elsif v_marks between 900 and 989 then
        v_class := 'First Class';
    elsif v_marks between 825 and 899 then
        v_class := 'Higher Second Class';
    else
        v_class := 'Pass';
    end if;

    insert into result values (p_roll, v_name, v_class);
    commit;
end;
/
```
```
declare
    r number := &roll_no;
begin
    proc_grade(r);
end;
/
```
```
Select * from results;
```
