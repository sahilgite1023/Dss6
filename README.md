# Dss6

Assignment 6

Study & Implementation of PL/SQL

Write a PL/SQL block or code for the following requirements:-
1) Accept rollno from user.
2) Retrieve name and percentage of the students with rollno given by user.
3) Calculate grade of that student as per follows:

Percentage >= 80 then grade = A+
Percentage >= 70 and < 80 then grade = A
Percentage >= 60 and < 70 then grade = B+
Percentage >= 50 and < 60 then grade = B
Percentage >= 40 and < 50 then grade = C
Percentage below 40 then grade = Fail

Display all details of student and grade.
Use appropriate control structure and exception handling.









CREATE TABLE student (
    rollno NUMBER PRIMARY KEY,
    name VARCHAR2(50),
    percentage NUMBER(5,2)
);

INSERT INTO student VALUES (1,'Anil',85);
INSERT INTO student VALUES (2,'Pritee',75);
INSERT INTO student VALUES (3,'Rahul',66);
INSERT INTO student VALUES (4,'Priya',55);
INSERT INTO student VALUES (5,'Rohit',45);
INSERT INTO student VALUES (6,'Kiran',32);

DECLARE
    v_rollno student.rollno%TYPE := &rollno;
    v_name student.name%TYPE;
    v_percentage student.percentage%TYPE;
    v_grade VARCHAR2(10);

BEGIN
    SELECT name, percentage
    INTO v_name, v_percentage
    FROM student
    WHERE rollno = v_rollno;

    IF v_percentage >= 80 THEN
        v_grade := 'A+';
    ELSIF v_percentage >= 70 AND v_percentage < 80 THEN
        v_grade := 'A';
    ELSIF v_percentage >= 60 AND v_percentage < 70 THEN
        v_grade := 'B+';
    ELSIF v_percentage >= 50 AND v_percentage < 60 THEN
        v_grade := 'B';
    ELSIF v_percentage >= 40 AND v_percentage < 50 THEN
        v_grade := 'C';
    ELSE
        v_grade := 'Fail';
    END IF;

    DBMS_OUTPUT.PUT_LINE('Roll No : ' || v_rollno);
    DBMS_OUTPUT.PUT_LINE('Name : ' || v_name);
    DBMS_OUTPUT.PUT_LINE('Percentage : ' || v_percentage);
    DBMS_OUTPUT.PUT_LINE('Grade : ' || v_grade);

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Student not found');

    WHEN TOO_MANY_ROWS THEN
        DBMS_OUTPUT.PUT_LINE('Multiple students found');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error occurred : ' || SQLERRM);

END;




/
