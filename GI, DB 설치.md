# GI, DB 설치
-------------
 
* 비용 들여 mirroring 하면 디스크가 손상되어도 이용 가능
*   
* 1) GI 설치
	* [PROD@host01 ~]$ cd /stage/grid
	* [PROD@host01 grid]$ ./runInstaller
	*  
	* ![gi 1](https://user-images.githubusercontent.com/58458582/84277042-f21d1a80-ab6d-11ea-89dd-9082cca4a24d.PNG)
	* ![gi 2](https://user-images.githubusercontent.com/58458582/84277045-f2b5b100-ab6d-11ea-868f-6d933dcf59ea.PNG)
	* ![gi 설치](https://user-images.githubusercontent.com/58458582/84277048-f34e4780-ab6d-11ea-9a16-d9a2f243e547.PNG)
	*  
	* [root@host01 ~]# /u01/app/oraInventory/orainstRoot.sh
	* [root@host01 ~]# /u01/app/oracle/product/11.2.0.3/grid/root.sh
	* [root@host01 ~]# exit
	*  
	* [PROD@host01 grid]$ . oraenv
	* ORACLE_SID = [PROD] ? +ASM
	* [+ASM@host01 grid]$ asmca
	* ![asm 1](https://user-images.githubusercontent.com/58458582/84276961-e29dd180-ab6d-11ea-9e5a-0c9a1f30396b.PNG)
		* +DATA : 내가 관리할 필요 X
		* ASM 디스크 그룹 : 경합 X -> 안정성 확보, 모두 균등하게 사용
	* ![asm 2 - mirroring 안함](https://user-images.githubusercontent.com/58458582/84276962-e29dd180-ab6d-11ea-8eca-72a5b80842e8.PNG)
		*  normal 은 데이터를 이중화시켜서 물리적디스크손상이생겨도 디비가 굴러갈수있게 함
		* high 는 3중화
		* externel은 그런게 없음
	* ![asm 3 만든 결과](https://user-images.githubusercontent.com/58458582/84276966-e3366800-ab6d-11ea-800d-7a2d6c855410.PNG)

* 2) DB 설치
	* [PROD@host01 ~]$ cd /stage/database
	* [PROD@host01 database]$ ./runInstaller
	*  
	* ![db 설치 1](https://user-images.githubusercontent.com/58458582/84276997-e9c4df80-ab6d-11ea-949b-e348801c940a.PNG)
		* DB software 설치
	* ![db 설치 2](https://user-images.githubusercontent.com/58458582/84276998-e9c4df80-ab6d-11ea-818d-e238eecec34a.PNG)
	* ![db 설치 3](https://user-images.githubusercontent.com/58458582/84276999-ea5d7600-ab6d-11ea-8e8e-d90face252a6.PNG)
	* ![db 설치 4](https://user-images.githubusercontent.com/58458582/84277000-eaf60c80-ab6d-11ea-8c3c-48121e573c70.PNG)
	* ![db 설치 5](https://user-images.githubusercontent.com/58458582/84277001-eaf60c80-ab6d-11ea-8e0d-8ef6ef2c095b.PNG)
	* ![db 설치 6](https://user-images.githubusercontent.com/58458582/84277003-eb8ea300-ab6d-11ea-8148-c9b4f7207045.PNG)
	* ![db 설치 7](https://user-images.githubusercontent.com/58458582/84277006-ec273980-ab6d-11ea-8594-52502c10fa81.PNG)
	* ![db 설치 8](https://user-images.githubusercontent.com/58458582/84277010-ecbfd000-ab6d-11ea-9f0e-910654cee183.PNG)

* 3) DB 생성
	* [PROD@host01 ~]$ dbca
	*  
	* ![dbca 1](https://user-images.githubusercontent.com/58458582/84277011-ecbfd000-ab6d-11ea-9519-610de615457f.PNG)
	* ![dbca 2](https://user-images.githubusercontent.com/58458582/84277014-ed586680-ab6d-11ea-92e8-4953ab5e178c.PNG)
	* ![dbca 3](https://user-images.githubusercontent.com/58458582/84277016-edf0fd00-ab6d-11ea-8a89-27e22741dab4.PNG)
	* ![dbca 4 em üũ](https://user-images.githubusercontent.com/58458582/84277018-edf0fd00-ab6d-11ea-99f6-6f50bc323620.PNG)
		* EM 체크
	* ![dbca 5](https://user-images.githubusercontent.com/58458582/84277019-ee899380-ab6d-11ea-9a8e-c1a0dee6b9b9.PNG)
	* ![dbca 6-1](https://user-images.githubusercontent.com/58458582/84277021-ee899380-ab6d-11ea-8f27-b092e850bd91.PNG)
	* ![dbca6 asm, +data](https://user-images.githubusercontent.com/58458582/84277035-f1848400-ab6d-11ea-8c75-052ab6dd188f.PNG)
		* ASM, +DATA 지정
	* ![dbca 7](https://user-images.githubusercontent.com/58458582/84277022-ef222a00-ab6d-11ea-8e47-7b8163e16cec.PNG)
	* ![dbca 8](https://user-images.githubusercontent.com/58458582/84277026-efbac080-ab6d-11ea-9e27-a35b7ead0840.PNG)
	* ![dbca 9](https://user-images.githubusercontent.com/58458582/84277027-efbac080-ab6d-11ea-9195-782e6130024d.PNG)
	* ![dbca 10](https://user-images.githubusercontent.com/58458582/84277028-f0535700-ab6d-11ea-8468-9d88462aeae9.PNG)
	* ![dbca 11](https://user-images.githubusercontent.com/58458582/84277030-f0ebed80-ab6d-11ea-86b4-71718e20645a.PNG)
	* ![dbca 12](https://user-images.githubusercontent.com/58458582/84277033-f0ebed80-ab6d-11ea-871a-278ffeaa04cb.PNG)

