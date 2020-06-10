# single db on ASM
-------------

* ASM 사용하려면 GI 설치 필요
* GI는 스토리지 관리하기 위한 것
*  
* [root@host01 ~]# vi /home/oracle/.bash_profile
* ![asm 4](https://user-images.githubusercontent.com/58458582/84276967-e3366800-ab6d-11ea-9d89-04a563312ba2.PNG)
*  
* [root@host01 ~]# mkdir -p /u01/app/oracle
* [root@host01 ~]# chown -R oracle:oinstall /u01
* [root@host01 ~]# chmod -R 775 /u01
*  
* [root@host01 ~]# rpm -qa oracleasm*
* ![asm 5](https://user-images.githubusercontent.com/58458582/84276968-e3cefe80-ab6d-11ea-92fc-5dc329b6be2c.PNG)
*  
* 내용들 잘 있나 확인
* [root@host01 ~]# cat /etc/sysctl.conf
* ![asm 6](https://user-images.githubusercontent.com/58458582/84276969-e4679500-ab6d-11ea-927e-227af065a68a.PNG)
*  [root@host01 ~]# cat /etc/security/limits.conf
* ![asm 7](https://user-images.githubusercontent.com/58458582/84276971-e4679500-ab6d-11ea-9461-6cdcde1415ea.PNG)
* [root@host01 ~]# cat /etc/hosts
* ![asm 8](https://user-images.githubusercontent.com/58458582/84276973-e5002b80-ab6d-11ea-9518-80165f058535.PNG)
*  
* [root@host01 ~]# mkdir -p /u02/asmdisks
* [root@host01 ~]# chown -R oracle:oinstall /u02/asmdisks
* [root@host01 ~]# chmod 666 /u02/asmdisks
*   
* [root@host01 ~]# cd /u02/asmdisks
* ![asm 9](https://user-images.githubusercontent.com/58458582/84276974-e598c200-ab6d-11ea-9f5b-3865e95b03fd.PNG)
*  
* [root@host01 asmdisks]# vi /etc/modprobe.conf
* 문장 추가
* options loop max_loop=32
*  
* ![asm 10](https://user-images.githubusercontent.com/58458582/84276976-e598c200-ab6d-11ea-9a4f-1ef7e76502b9.PNG)
* ![asm 11](https://user-images.githubusercontent.com/58458582/84276977-e6315880-ab6d-11ea-93a4-35e49ef13c2e.PNG)
*  
* [root@host01 asmdisks]# chmod 777 /etc/rc5.d/S91ora_start
* [root@host01 asmdisks]# reboot
*  
* [root@host01 ~]# ls -l /dev/xv*
* ![asm 12](https://user-images.githubusercontent.com/58458582/84276979-e6315880-ab6d-11ea-9dc0-99c35fc2bde0.PNG)
*  
* [root@host01 ~]# oracleasm configure -i
* ![asm 13](https://user-images.githubusercontent.com/58458582/84276981-e6c9ef00-ab6d-11ea-9c4d-31927d114c7f.PNG)
*  
* [root@host01 ~]# oracleasm exit
* [root@host01 ~]# oracleasm init
* ![asm 14](https://user-images.githubusercontent.com/58458582/84276983-e7628580-ab6d-11ea-93df-603ca513c58e.PNG)
*  
* [root@host01 ~]# oracleasm status
* ![asm 15](https://user-images.githubusercontent.com/58458582/84276985-e7628580-ab6d-11ea-875b-1cdb8147a01f.PNG)
*  
* ![asm 16](https://user-images.githubusercontent.com/58458582/84276987-e7fb1c00-ab6d-11ea-9eb1-ba7ed6df853b.PNG)
*  
* [root@host01 ~]# oracleasm scandisks
* ![asm 17](https://user-images.githubusercontent.com/58458582/84276990-e7fb1c00-ab6d-11ea-9f5a-3efda3dece82.PNG)
*  
* [root@host01 ~]# oracleasm listdisks
* ![asm 18](https://user-images.githubusercontent.com/58458582/84276992-e893b280-ab6d-11ea-9b34-9f0df05f57c9.PNG)
*  
* [root@host01 ~]# shutdown -h now

