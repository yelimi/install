db 설치
-------------

![db 설치 1](https://user-images.githubusercontent.com/58458582/84183849-736da200-aac7-11ea-9ba1-7e2d7e6f6ee8.PNG)

* [PROD@localhost ~]$ cd /stage/database/
* [PROD@localhost database]$ ./runInstaller
* db 설치창 뜨면 설정 후 설치


db 생성
-------------

* [PROD@localhost ~]$ dbca
* 생성창 뜨면 설정 후 생성
* 리스너 생성
	* [PROD@localhost ~]$ netca


db 삭제 후 재생성
-------------
 
* [PROD@hosㄴ t01 ~]$ sqlplus / as sysdba
*  
* SQL> shutdown immediate
* SQL> startup mount exclusive restrict
*  
* SQL> drop database;
* SQL> exit;
*  
* [PROD@host01 ~]$ ls -l /u01/app/oracle/oradata/PROD
* (결과)  total 0
* [PROD@host01 ~]$ ls -l $ORACLE_HOME/dbs
* (결과)  total 16
	* (결과) -rw-rw---- 1 oracle oinstall 1544 Jun  5 17:46 hc_PROD.dat
	* -rw-r--r-- 1 oracle oinstall 2851 May 15  2009 init.ora
	* -rw-r----- 1 oracle oinstall   24 Jun  5 17:46 lkPROD
	* -rw-r----- 1 oracle oinstall 1536 Jun  5 17:50 orapwPROD
*  
* [PROD@host01 ~]$ rm -rf /u01/app/oracle/oradata/PROD
* [PROD@host01 ~]$ mkdir -p /u01/app/oracle/oradata/PROD
*  
* [PROD@host01 ~]$ cd $ORACLE_HOME/dbs
*  
* [PROD@host01 dbs]$ rm orapwPROD
* [PROD@host01 dbs]$ orapwd file=orapwPROD password=oracle_4U
*  
* ![00](https://user-images.githubusercontent.com/58458582/84183823-6d77c100-aac7-11ea-8567-32cfdf02bba8.PNG)
*  
* [PROD@host01 dbs]$ sqlplus / as sysdba
*  
* SQL> CREATE SPFILE FROM PFILE ;
* SQL> STARTUP NOMOUNT
* ![01](https://user-images.githubusercontent.com/58458582/84183831-6f418480-aac7-11ea-8ccf-731a2e39f325.PNG)
*  
* SQL> @?/rdbms/admin/catalog.sql
* SQL> @?/rdbms/admin/catproc.sql
* SQL> connect  system/oracle_4U
* SQL> @?/sqlplus/admin/pupbld.sql
* SQL> exit

