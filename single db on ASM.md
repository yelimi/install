# single db on ASM
-------------

* 먼저 하드 디스크 4개 생성
*  
* [root@host01 ~]# vi /home/oracle/.bash_profile
* ![asm1](https://user-images.githubusercontent.com/58458582/84409686-b2773100-ac48-11ea-95f8-bd9b30da2e7f.PNG)
*  
* [root@host01 ~]# mkdir -p /u01/app/oracle
* [root@host01 ~]# chown -R oracle:oinstall /u01
* [root@host01 ~]# chmod -R 775 /u01
*  
* [root@host01 ~]# rpm -qa oracleasm*
* ![asm2](https://user-images.githubusercontent.com/58458582/84409689-b3a85e00-ac48-11ea-971e-9b3e413e61cb.PNG)
*  
* [root@host01 ~]# cat /etc/sysctl.conf
* ![asm3](https://user-images.githubusercontent.com/58458582/84409691-b440f480-ac48-11ea-87bb-6ad0a1ac648d.PNG)
* [root@host01 ~]# cat /etc/security/limits.conf
* ![asm4](https://user-images.githubusercontent.com/58458582/84409695-b4d98b00-ac48-11ea-8124-77d54030d60d.PNG)
* [root@host01 ~]# cat /etc/hosts
* ![asm5](https://user-images.githubusercontent.com/58458582/84409696-b5722180-ac48-11ea-9f6d-afbcaf53c071.PNG)
*  
* // disk 준비
* [root@host01 ~]# fdisk /dev/sdb
* ![asm6](https://user-images.githubusercontent.com/58458582/84409697-b5722180-ac48-11ea-90f7-8b4790ab719f.PNG)
* [root@host01 ~]# fdisk /dev/sdc
	* 위와 같은 방식으로
* [root@host01 ~]# fdisk /dev/sdd
	* 위와 같은 방식으로
* [root@host01 ~]# fdisk /dev/sde
	* 위와 같은 방식으로
*  
* // ASM DISK 준비
* [root@host01 ~]# oracleasm configure -i
* ![asm7](https://user-images.githubusercontent.com/58458582/84409703-b60ab800-ac48-11ea-8dad-17d68b3a3544.PNG)
*  
* [root@host01 ~]# oracleasm createdisk ASMDISK01 /dev/sdb1
* [root@host01 ~]# oracleasm createdisk ASMDISK02 /dev/sdc1
* [root@host01 ~]# oracleasm createdisk ASMDISK03 /dev/sdd1
* [root@host01 ~]# oracleasm createdisk ASMDISK04 /dev/sde1
* [root@host01 ~]# oracleasm exit
* [root@host01 ~]# oracleasm init
* [root@host01 ~]# oracleasm scandisks
* ![asm8](https://user-images.githubusercontent.com/58458582/84409706-b6a34e80-ac48-11ea-96d1-46a0f7586f69.PNG)
* createdisk 에러 발생 시(failed) oracleasm listdisks까지 실행 후 다시 생성 할 것 (scandisks시 아무것도 안나오면 다시 생성)
*  
* [root@host01 ~]# oracleasm status
* ![asm9](https://user-images.githubusercontent.com/58458582/84409708-b73be500-ac48-11ea-8190-168a52587e5e.PNG)
*  
* [root@host01 ~]# reboot
*  
* [root@host01 ~]# oracleasm listdisks
* ![asm8](https://user-images.githubusercontent.com/58458582/84409706-b6a34e80-ac48-11ea-96d1-46a0f7586f69.PNG)
*  
* GI 설치
* DATA, FRA Disk Group 생성 
* DB 설치 
* DB 생성

