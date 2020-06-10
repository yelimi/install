# single db_lvm (logical volume device)
-------------

* 하나의 큰 space 안에 여러 개가 그룹화

* 1) db 설치 준비
	* [root@host01 ~]# groupadd oinstall
	* [root@host01 ~]# groupadd dba
	* [root@host01 ~]# groupadd oper
	* [root@host01 ~]# groupadd asmadmin
	* [root@host01 ~]# groupadd asmdba
	* [root@host01 ~]# groupadd asmoper
	*  
	* [root@host01 ~]# useradd -g oinstall -G dba,oper,asmdba,asmadmin,asmoper oracle
	*  
	* [root@host01 ~]# passwd oracle
	*  
	* [root@host01 ~]# vi /home/oracle/.bash_profile
	* 문장  추가
	* ![설치 준비 1](https://user-images.githubusercontent.com/58458582/84277812-f564d600-ab6e-11ea-9122-436f1216b78c.PNG)
	*  
	* [root@host01 ~]# chown oracle:oinstall /home/oracle/.bash_profile
	*  
	* 리눅스 dvd 마운트
		* ![설치 준비 8](https://user-images.githubusercontent.com/58458582/84277840-fa298a00-ab6e-11ea-961b-13a0e7a9abab.PNG)
	*  
	* [root@host01 Server]# cd /media/Enterprise\ Linux\ dvd\ 20090908/Server/
	* 문장 입력
	* ![설치 준비 2](https://user-images.githubusercontent.com/58458582/84277817-f6960300-ab6e-11ea-961c-553a8a0d9551.PNG)
	*  
	* [root@host01 Server]# cd /mnt/hgfs/share
	* [root@host01 share]# tar xvzf rpm.tar.gz
	* 문장 입력
	* ![설치 준비 3](https://user-images.githubusercontent.com/58458582/84277820-f72e9980-ab6e-11ea-8516-373b82ac71b7.PNG)
	*  
	* [root@host01 share]# cd rpm
	* 문장 입력
	* ![설치 준비 4](https://user-images.githubusercontent.com/58458582/84277825-f72e9980-ab6e-11ea-9479-fdfb5685d719.PNG)
	*  
	* [root@host01 rpm]# vi /etc/sysctl.conf
	* 문장 추가
	* ![설치 준비 5](https://user-images.githubusercontent.com/58458582/84277832-f8f85d00-ab6e-11ea-9ecf-dbd71c0a4444.PNG)
	*  
	* [root@host01 rpm]# vi /etc/security/limits.conf
	* 문장 추가
	* ![설치 준비 6](https://user-images.githubusercontent.com/58458582/84277834-f990f380-ab6e-11ea-8678-071af58d3eff.PNG)
	*  
	* [root@host01 rpm]# vi /etc/hosts
	* 문장 추가
	* ![설치 준비 7](https://user-images.githubusercontent.com/58458582/84277837-f990f380-ab6e-11ea-9018-8eeb88f6520f.PNG)
	*  
	* [root@host01 rpm]# mv /etc/ntp.conf /etc/ntp.conf.org
	*  
	* [root@host01 rpm]# mkdir -p /u01/app/oracle
	* [root@host01 rpm]# chown -R oracle:oinstall /u01
	* [root@host01 rpm]# chmod -R 775 /u01
	*  
	* [root@host01 rpm]# mkdir /stage
	* [root@host01 rpm]# cd /mnt/hgfs/share
	*  
	* [root@host01 share]# unzip  p10404530_112030_Linux-x86-64_1of7.zip -d /stage
	* [root@host01 share]# unzip  p10404530_112030_Linux-x86-64_2of7.zip -d /stage
	* [root@host01 share]# chown -R oracle:oinstall  /stage

* 2) Logical Volume Device
	* [root@host01 ~]# rpm -qa | grep lvm
	* (결과) lvm2-2.02.46-8.el5   ,    system-config-lvm-1.1.5-1.0.el5
		* 패키지 확인
	*  
	* [root@host01 ~]# fdisk -l
	* ![lvm 1](https://user-images.githubusercontent.com/58458582/84277049-f34e4780-ab6d-11ea-907a-5d2e30ae1121.PNG)
		* 내용, 공간 확인
	*  
	* [root@host01 ~]# fdisk /dev/sdb
	* ![lvm 2](https://user-images.githubusercontent.com/58458582/84277051-f3e6de00-ab6d-11ea-9961-ef30d9ef785b.PNG)
	* [root@host01 ~]# fdisk /dev/sdc
		* 위의 사진과 동일한 방법으로
	* [root@host01 ~]# fdisk /dev/sdd
		* 위의 사진과 동일한 방법으로
	* [root@host01 ~]# fdisk -l
	* ![lvm 3](https://user-images.githubusercontent.com/58458582/84277053-f3e6de00-ab6d-11ea-8a6d-8ce62076a2e2.PNG)
		* 파티션이 만들어졌음을 확인 가능
	*  
	* [root@host01 ~]# pvcreate /dev/sdb1
	* [root@host01 ~]# pvcreate /dev/sdc1
	* [root@host01 ~]# pvcreate /dev/sdd1
		* physical volume 생성
	*  
	* [root@host01 ~]# pvdisplay
	* ![lvm 4](https://user-images.githubusercontent.com/58458582/84277054-f47f7480-ab6d-11ea-82db-b23d9d5d54e4.PNG)
		* physical volume 목록 보여줌
	*  
	* [root@host01 ~]# vgcreate vg01 /dev/sdb1 /dev/sdc1 /dev/sdd1
		* volume group 안에 3개의 physical volume이 포함되도록 생성
	*  
	* [root@host01 ~]# vgdisplay
	* ![lvm 5](https://user-images.githubusercontent.com/58458582/84277056-f5180b00-ab6d-11ea-9aad-aa237bcd1dc1.PNG)
	*  
	* logical volume 생성하도록 입력
	* ![lvm 6](https://user-images.githubusercontent.com/58458582/84277059-f5b0a180-ab6d-11ea-975b-8f6571c5adb6.PNG)
	*  
	* [root@host01 ~]# lvscan -v 
	* ![lvm 7](https://user-images.githubusercontent.com/58458582/84277060-f5b0a180-ab6d-11ea-955a-a29548c7f34e.PNG)
		* 정보 확인
	*  
	* [root@host01 ~]# lvdisplay
	* ![lvm 8](https://user-images.githubusercontent.com/58458582/84277062-f6493800-ab6d-11ea-8821-48996b75e70e.PNG)
	*  
	* [root@host01 ~]# rm -rf >> /etc/rc5.d/S91ora_start << EOF 
		* 잘 안됐을 경우
	* [root@host01 ~]# cat >> /etc/rc5.d/S91ora_start << EOF
	* #!/bin/bash
	* 문장 입력
	* ![lvm 9](https://user-images.githubusercontent.com/58458582/84277063-f6493800-ab6d-11ea-8c53-b1444816d241.PNG)
	* ![lvm 10](https://user-images.githubusercontent.com/58458582/84277065-f6e1ce80-ab6d-11ea-9dc4-8f2c9bec5959.PNG)
	*   
	* [root@host01 ~]# chmod 777 /etc/rc5.d/S91ora_start
	* [root@host01 ~]# reboot
	*  
	* [root@host01 ~]# /bin/raw -qa
	* ![lvm 11](https://user-images.githubusercontent.com/58458582/84277069-f77a6500-ab6d-11ea-955d-7bd91791583f.PNG)
	*  
	* [root@host01 ~]# ls -l /dev/raw/raw*

* 3) db 설치
* 4) db 생성
	* [PROD@host01 ~]$ mkdir -p /u01/app/oracle/oradata/PROD
	*  
	* [PROD@host01 ~]$ cd $ORACLE_HOME/dbs
	*  
	* [PROD@host01 dbs]$ orapwd file=orapwPROD password=oracle_4U
	*  
	* ![lvm 12](https://user-images.githubusercontent.com/58458582/84277070-f812fb80-ab6d-11ea-93d7-de579752e381.PNG)
	*  
	* [PROD@host01 dbs]$ sqlplus / as sysdba
	*  
	* SQL> CREATE SPFILE FROM PFILE ;
	* SQL> STARTUP NOMOUNT
	* ![lvm 13](https://user-images.githubusercontent.com/58458582/84277075-f812fb80-ab6d-11ea-884b-547a94f1258e.PNG)
	*  
	* SQL> @?/rdbms/admin/catalog.sql
	* SQL> @?/rdbms/admin/catproc.sql
	* SQL> connect  system/oracle_4U
	* SQL> @?/sqlplus/admin/pupbld.sql
	*  
	* SQL> exit
	*  
	* [PROD@host01 dbs]$ vi /etc/oratab
	* 문장 추가
	* PROD:/u01/app/oracle/product/11.2.0.3/dbhome:N

