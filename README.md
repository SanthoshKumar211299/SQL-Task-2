mysql-EER DIAGRAM:
------------------

DESIGN DB MODEL FOR GUVI ZEN CLASS
----------------------------------

— create database zen_class;
----------------------------

use zen_class;

—User table:
------------

create table users(

user_id integer auto_increment primary key,

user_name varchar (255),

email varchar (255),

createdAt datetime,

batch integer

);

— to view table

select * from users;

— to insert table data

INSERT INTO users (user_name, email, createdAt, batch)

VALUES (‘karthik’,’karthi@gmail.com’,CURRENT_TIMESTAMP(),1),

(‘gayu’,’gayu@gmail.com’,CURRENT_TIMESTAMP(),2),

(‘maha’,’maha@gmail.com’,CURRENT_TIMESTAMP(),3),

(‘mugilan’,’mugil@gmail.com’,CURRENT_TIMESTAMP(),4),

(‘iniya’,’iniya@gmail.com’,CURRENT_TIMESTAMP(),5);

— if u want to delete only table data use this query

delete from users where user_id in(1,2,3,4,5);

— if u have to refer another foreign key

alter table users

add foreign key (batch) references batch_data (batch_id);

— table codekata:
-----------------------

create table codekata(

code_id integer auto_increment primary key,

user_id integer,

number_of_problem integer,

status_problem varchar(255),

FOREIGN KEY (user_id) REFERENCES users(user_id)

);

delete from codekata where code_id in(6,7,8,9,10);

select * from codekata;

drop table codekata;

INSERT INTO codekata( user_id,number_of_problem,status_problem) VALUES

(6,20,’pending’),

( 6,20,’finished’),

(7,40,’finished’),

(7,40,’finished’),

(8,50,’finished’);

select * from codeketa;

delete from codeketa where code_id in(2,3,4,5);

delete from users where user_id in(1,2,3,4,5);

DELETE FROM codeketa;

— Primary keys must contain UNIQUE values, and cannot contain NULL values.

— The table with the foreign key is called the child table, and

— the table with the primary key is called the referenced or parent table.

— company_drives:
-----------------

CREATE TABLE company_drives (

drive_id INTEGER AUTO_INCREMENT PRIMARY KEY,

user_id INTEGER,

drive_date DATE,

company VARCHAR(100),

FOREIGN KEY (user_id) REFERENCES users(user_id)

);

INSERT INTO company_drives(user_id, drive_date, company) VALUES

(6,makedate(2024, 3), “Apple”),

(6,makedate(2024, 5), “Amazon”),

(7,makedate(2024, 3), “Zomato”),

(7,makedate(2023, 12), “Flipkart”),

(8,makedate(2023,5), “TCS”);

select * from company_drives;

delete from company_drives where user_id in(1,2,3,4,5);

Batch Table:
------------

CREATE TABLE batch_data(

batch_id int auto_increment primary key,

batch_name varchar(100)

);

insert into batch_data(batch_name)values

(‘full stack-2023’),

(‘full stack-2023’),

(‘html-2023’),

(‘css-2023’),

(‘mongodb-2023’);

select * from batch_data;

alter table batch_data

add foreign key (batch_id)references users(batch);

— inner join table-common value

SELECT users.batch,batch_data.batch_id

FROM users

INNER JOIN batch_data on users.batch = batch_data.batch_id;

— mentor table:
--------------

CREATE TABLE mentors (

mentor_id INTEGER AUTO_INCREMENT PRIMARY KEY,

mentor_name VARCHAR(100),

mentor_email VARCHAR(100)

);

INSERT INTO mentors(mentor_name, mentor_email) VALUES

(“Surya”, “suryakumar@gmail.com”),

(“Viji” , “vijay@gmail.com”),

(“arun”,”arun@gmail.com”),

(“prabhu” ,”prabhu@gmail.com”);

INSERT INTO mentors(mentorname, mentoremail) VALUES

(“naga”,”naga@gmail.com”);

select * from mentors;

— table topics:
----------------------

CREATE TABLE topics (

topic_id INT PRIMARY KEY,

topic VARCHAR(200),

topic_date DATE,

mentor_id int,

FOREIGN KEY (mentor_id) REFERENCES mentors(mentor_id)

);

INSERT INTO topics(topic, topic_date, mentor_id) VALUES

(“HTML — Basics”, “2023–04–01”, 1),

(“NodeJS — Basics”, “2023–06–03”, 2),

(“JavaScript — Basics”, “2023–07–05”, 3),

(“React — Basics”, “2023–08–06”, 4),

(“mysql -Basic”,”2023–09–5",5);

select * from topics;

— tasks table:
---------------

CREATE TABLE tasks (

taskid INT PRIMARY KEY,

topic_id int,

task VARCHAR(1000),

batch_id INT,

FOREIGN KEY (topic_id) REFERENCES topics(topic_id)

);

INSERT INTO tasks(topic_id, task, batch_id)VALUES

(1, “HTML Task”, 1),

(2, “Javascript Task”, 2),

(3, “React Task”,3),

(4, “NodeJs Task”,4),

(5, “Mysql task”,5);

select * from tasks;

attendance table:
--------------------

CREATE TABLE attendance (

attendance_id INT PRIMARY KEY,

user_id integer,

topicsid INTEGER,

attended BOOLEAN,

FOREIGN KEY ( user_id) REFERENCES users( user_id),

FOREIGN KEY (topic_id) REFERENCES topics(topic_id)

);

INSERT INTO attendance( user_id, topicsid, attended) VALUES

(6, 3, true),

(6, 1, true),

(7, 2, false),

(7, 4, true),

(8, 4, true);

select * from attendance;
