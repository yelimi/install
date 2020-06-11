# 11.2.0.3 to 11.2.0.4 (update)
-------------

* 1) upgrade GI from 11.2.0.3 to 11.2.0.4
	* [PROD@host01 ~]$ cd /mnt/hgfs/share 
	*  
	* [PROD@host01 share]$ mkdir -p /stage/11.2.0.4
	* [PROD@host01 share]$ unzip -d /stage/11.2.0.4 p13390677_112040_Linux-x86-64_3of7.zip 
	* [PROD@host01 share]$ unzip -d /stage/11.2.0.4 p13390677_112040_Linux-x86-64_1of7.zip
	* [PROD@host01 share]$ unzip -d /stage/11.2.0.4 p13390677_112040_Linux-x86-64_2of7.zip
	*  
	* [PROD@host01 share]$ mkdir -p /u01/app/oracle/product/11.2.0.4/grid
	* [PROD@host01 share]$ mkdir -p /u01/app/oracle/product/11.2.0.4/dbhome
	*  
	* [PROD@host01 share]$ cd /stage/11.2.0.4/grid
	* [PROD@host01 grid]$ unset ORACLE_HOME
	* [PROD@host01 grid]$ unset ORACLE_BASE
	* [PROD@host01 grid]$ unset ORACLE_SID
	*  
	* [@host01 grid]$ ./runInstaller
	* ![u_gi 1](https://user-images.githubusercontent.com/58458582/84409777-bdca5c80-ac48-11ea-99f5-64ec05c68ff1.PNG)
	* ![u_gi 2](https://user-images.githubusercontent.com/58458582/84409782-be62f300-ac48-11ea-989c-30fb126a84ed.PNG)
	* ![u_gi 3](https://user-images.githubusercontent.com/58458582/84409786-befb8980-ac48-11ea-9ba0-d841d28f9b7e.PNG)
	* [root@host01 ~]# /u01/app/oracle/product/11.2.0.4/grid/rootupgrade.sh
	* ![u_gi 4](https://user-images.githubusercontent.com/58458582/84409790-befb8980-ac48-11ea-8f74-11c60e075863.PNG)
	*  
	* // GI 현재 버전 확인
	* [@host01 grid]$ crsctl query has softwareversion
	* (결과)   Oracle High Availability Services version on the local node is [11.2.0.4.0]
	*  
	* // change user grid .bash_profile
	* [@host01 grid]$ cd
	* [@host01 ~]$ vi .bash_profile
	* 3 -> 4 변경
	* ![u_gi 5](https://user-images.githubusercontent.com/58458582/84409801-bf942000-ac48-11ea-979a-003b179ed51d.PNG)
* 2) upgrade database from 11.2.0.3 to 11.2.0.4
	* // db software 설치
	* [@host01 ~]$ cd /stage/11.2.0.4/database
	* [@host01 database]$ ./runInstaller
	* ![u_db 1](https://user-images.githubusercontent.com/58458582/84409743-bb680280-ac48-11ea-8c3a-6a4516d24472.PNG)
	* ![u_db 2](https://user-images.githubusercontent.com/58458582/84409745-bc009900-ac48-11ea-8141-52c10692d2b3.PNG)
	* ![u_db 3](https://user-images.githubusercontent.com/58458582/84409748-bc992f80-ac48-11ea-823c-36e1a9f90599.PNG)
	* ![u_db 4](https://user-images.githubusercontent.com/58458582/84409752-bc992f80-ac48-11ea-9492-5868b0224d31.PNG)
	* ![u_db 5](https://user-images.githubusercontent.com/58458582/84409757-bd31c600-ac48-11ea-93f0-1ac8b61ecd3c.PNG)
	* ![u_db 6](https://user-images.githubusercontent.com/58458582/84409764-bd31c600-ac48-11ea-8ebc-262bcccd083f.PNG)
	* [PROD@host01 ~]$ su -
	* [root@host01 ~]# /u01/app/oracle/product/11.2.0.4/dbhome/root.sh
	* ![u_db7](https://user-images.githubusercontent.com/58458582/84409770-bdca5c80-ac48-11ea-9c16-7d65aed85505.PNG)
	* [root@host01 ~]# exit
	*  
	* // run utlu112i.sql before upgrade
	* [PROD@host01 ~]$ export ORACLE_BASE=/u01/app/oracle 
	* [PROD@host01 ~]$ export ORACLE_HOME=/u01/app/oracle/product/11.2.0.3/dbhome
	* [PROD@host01 ~]$ export ORACLE_SID=PROD
	*  
	* [PROD@host01 ~]$ sqlplus / as sysdba
	* SQL> @/u01/app/oracle/product/11.2.0.4/dbhome_1/rdbms/admin/utlu112i.sql
	* SQL> exit
	*  
	* // upgrade database by DBUA
	* [PROD@host01 ~]$ /u01/app/oracle/product/11.2.0.4/dbhome_1/bin/dbua
	* ![db step4 1](https://user-images.githubusercontent.com/58458582/84409710-b73be500-ac48-11ea-89b4-cd4412a8d620.PNG)
	* ![db step4 2](https://user-images.githubusercontent.com/58458582/84409713-b7d47b80-ac48-11ea-8bc7-2a74c44d691c.PNG)
	* ![db step4 3](https://user-images.githubusercontent.com/58458582/84409714-b86d1200-ac48-11ea-9753-b8b75b65cd4f.PNG)
	* ![db step4 4](https://user-images.githubusercontent.com/58458582/84409718-b86d1200-ac48-11ea-9199-e72d214072e8.PNG)
	*  
	* // do some verify
	* [PROD@host01 ~]$ cat /etc/oratab
	* ![db step4 5](https://user-images.githubusercontent.com/58458582/84409722-b905a880-ac48-11ea-82e0-71e6a1b7158e.PNG)
	*  
	* [PROD@host01 ~]$ . oraenv
	* ORACLE_SID = [PROD] ? PROD
	*  
	* ![db step4 6](https://user-images.githubusercontent.com/58458582/84409723-b905a880-ac48-11ea-8cd7-9631ee0c9cb2.PNG)
	*  
	* [PROD@host01 ~]$ sqlplus / as sysdba
	* SYS@PROD> col comp_name for a40
	* SYS@PROD> col version for a20
	* SYS@PROD> col status for a20
	* SYS@PROD> col schema for a15
	*  
	* SYS@PROD> SELECT comp_name,version,status,schema FROM dba_registry ;
	* ![db step4 7](https://user-images.githubusercontent.com/58458582/84409726-b99e3f00-ac48-11ea-98c7-611d7b36ab68.PNG)
	*  
	* SYS@PROD> SELECT owner,object_name,object_type,status FROM dba_objects WHERE status != 'VALID';
	* (결과) no rows selected
	*  
	* [PROD@host01 ~]$ su - root
	* [root@host01 ~]# rm -rf /u01/app/oracle/product/11.2.0.3

