## DNS 서버 역할
도메인에 속해 있는 컴퓨터들의 이름을 관리하고, 외부에 해당 컴퓨터의 IP주소를 알려주는 역할  
1. COM 네임 서버에 도메인을 등록한다. ex) smpark.com 도메인에 DNS 서버의 IP를 등록
2. 외부에서 www.smpark.com 접속
3. Root 네임 서버에 먼저 물어본다.
4. COM 네임 서버에 물어본다.
5. 등록해놓은 smpark.com 도메인이 있으므로 DNS 서버의 IP를 가져온다.
6. DNS 서버 IP에 www.smpark.com의 IP를 물어본다.
7. 알아낸 www.smpark.com의 IP로 접속한다.

### 그림 참고
![1](https://raw.githubusercontent.com/smpark1020/tistory/master/CS/%5B%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%5D%20DNS%20Round%20Robin%20%EB%B0%A9%EC%8B%9D/1.PNG)

## 라운드 로빈(Round Robin) 방식의 DNS 서버
여러 대의 웹 서버를 운영해서 웹 클라이언트가 서비스를 요청할 경우에 교대로 서비스를 실시하도록 하는 방식   
대형 웹사이트에서 많이 사용한다.   
따라서 N대의 웹서버를 운영한다면 각 서버에 부하가 1/N으로 줄어든다.   
또한 혹시라도 1대의 웹서버가 죽더라도 약간 느려지긴 하겠지만 서비스는 이상없이 진행된다.   

### 그림 참고
![2](https://raw.githubusercontent.com/smpark1020/tistory/master/CS/%5B%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%5D%20DNS%20Round%20Robin%20%EB%B0%A9%EC%8B%9D/2.PNG)

## 참고
* [[이것이 Windows Server다] 10장 03교시 : DNS 서버 역할, 라운드 로빈 방식](https://youtu.be/7eV9T_NkCz0)
* [21/02/10 TL. Linux에서 마스터 네임 서버 구현(+라운드로빈). 웹 메일 서버 구현. 웹메일 설치](https://jerryk026.tistory.com/163)