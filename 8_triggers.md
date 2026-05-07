```
CREATE TABLE Library (
    Book_id NUMBER(10) PRIMARY KEY,
    Book_name VARCHAR2(100) NOT NULL,
    Author VARCHAR2(60),
    Status VARCHAR2(20),
    Issued_to VARCHAR2(50),
    Issue_date DATE,
    Return_date DATE
);
```
```
CREATE TABLE Library_Audit (
    Audit_id NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    Book_id NUMBER(10),
    Book_name VARCHAR2(100),
    Author VARCHAR2(60),
    Status VARCHAR2(20),
    Issued_to VARCHAR2(50),
    Issue_date DATE,
    Return_date DATE,
    Action VARCHAR2(10),
    Changed_on DATE DEFAULT SYSDATE
);
```
```
INSERT INTO Library VALUES 
(1001, 'DBMS Concepts', 'Ramez Elmasri', 'Available', NULL, NULL, NULL);
```
```
INSERT INTO Library VALUES 
(1002, 'OS Principles', 'Silberschatz', 'Issued', 'Alice', SYSDATE-5, SYSDATE+10);
```
```
COMMIT;
```
```
CREATE OR REPLACE TRIGGER trg_library_before_update
BEFORE UPDATE ON Library
FOR EACH ROW
BEGIN
    INSERT INTO Library_Audit (
        Book_id, Book_name, Author, Status,
        Issued_to, Issue_date, Return_date, Action
    ) VALUES (
        :OLD.Book_id, :OLD.Book_name, :OLD.Author, :OLD.Status,
        :OLD.Issued_to, :OLD.Issue_date, :OLD.Return_date, 'UPDATE'
    );
END;
/
```
```
CREATE OR REPLACE TRIGGER trg_library_before_delete
BEFORE DELETE ON Library
FOR EACH ROW
BEGIN
    INSERT INTO Library_Audit (
        Book_id, Book_name, Author, Status,
        Issued_to, Issue_date, Return_date, Action
    ) VALUES (
        :OLD.Book_id, :OLD.Book_name, :OLD.Author, :OLD.Status,
        :OLD.Issued_to, :OLD.Issue_date, :OLD.Return_date, 'DELETE'
    );
END;
/
```
```
CREATE OR REPLACE TRIGGER trg_library_after_insert
AFTER INSERT ON Library
FOR EACH ROW
BEGIN
    INSERT INTO Library_Audit (
        Book_id, Book_name, Author, Status,
        Issued_to, Issue_date, Return_date, Action
    ) VALUES (
        :NEW.Book_id, :NEW.Book_name, :NEW.Author, :NEW.Status,
        :NEW.Issued_to, :NEW.Issue_date, :NEW.Return_date, 'INSERT'
    );
END;
/
```
```
UPDATE Library 
SET Status = 'Issued', Issued_to = 'Bob'
WHERE Book_id = 1001;

COMMIT;
```
```
DELETE FROM Library 
WHERE Book_id = 1002;

COMMIT;
```
```
SELECT * FROM Library_Audit;
```
