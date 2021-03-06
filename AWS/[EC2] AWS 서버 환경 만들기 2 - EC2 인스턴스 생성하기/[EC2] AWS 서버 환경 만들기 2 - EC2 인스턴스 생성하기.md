EC2(Elastic Compute Cloud)는 AWS에서 제공하는 성능, 용량, 등을 유동적으로 사용할 수 있는 서버입니다.   
보통 "AWS에서 리눅스 서버 혹은 윈도우 서버를 사용합니다" 라고 하면 이 EC2를 이야기하는 것입니다.   

AWS에서 무료로 제공하는 프리티어 플랜에서는 EC2 사용에 다음과 같은 제한이 있습니다.   
* 사양이 t2.micro만 가능합니다.
  * vCPU(가상 CP) 1 Core, 메모리 1GB 사양입니다.
  * 보통 vCPU는 물리 CPU 사양의 절반 정도의 성능을 가집니다.
* 월 750시간의 제한이 있습니다.
  * 초과하면 비용이 부과됩니다.
  * 24시간 * 31일 = 744시간입니다.
  * 즉, 1대의 t2.micro만 사용한다면 24시간 사용할 수 있습니다.

위의 제한 사항을 주의하면서 AWS를 사용하면 1년간 재미나게 써볼 수 있습니다.   
EC2를 만들기 전에, 본인의 리전을 확인해 봅니다.   
> 리전이란 AWS의 서비스가 구동될 지역을 이야기합니다.
> AWS는 도시별로 클라우드 센터를 지어 해당 센터에서 구축된 가상머신들을 사용할 수 있습니다.   
> 이걸 리전이라고 합니다.   

다음과 같이 서울로 되어 있지 않다면 서울로 변경합니다.      
![1](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/1.PNG)   

검색창에 ec2를 입력하여 EC2 서비스를 클릭합니다.   
![2](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/2.PNG)

EC2 대시보드가 나오는데, 여기서 중앙에 있는 [인스턴스 시작] 버튼을 클릭합니다.   
인스턴스란 EC2 서비스에 생성된 가상머신을 이야기합니다.   
![3](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/3.PNG)

인스턴스를 생성하는 첫 단계는 AMI(Amazon Machine Image, 아마존 머신 이미지)를 선택하는 것입니다.   
먼저 AMI에 대해 설명하면, AMI는 EC2 인스턴스를 시작하는 데 필요한 정보를 이미지로 만들어 둔 것을 이야기합니다.   
인스턴스라는 가상 머신에 운영체제 등을 설치할 수 있게 구워 넣은 이미지로 생각하면 됩니다.   

Amazon Linux 2 AMI를 선택합니다.   
Amazon Linux 2 OS가 인스턴스에 설치되어 개발자가 사용할 수 있게 됩니다.   
![4](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/4.PNG)

아마존 리눅스 2는 센토스(Centos) 7 버전 자료들을 그대로 사용할 수 있습니다.   
센토스 AMI를 사용하지 않고 아마존 리눅스 AMI를 사용한 이유는 다음과 같습니다.
* 아마존이 개발하고 있기 때문에 지원받기가 쉽다.
* 레드햇 베이스이므로 레드햇 계열의 배포판을 많이 다뤄본 사람일수록 문제없이 사용할 수 있다.
* AWS의 각종 서비스와의 상성이 좋다.
* Amazon 독자적인 개발 리포지터리를 사용하고 있어 yum이 매우 빠르다.   

즉, AWS를 사용하는데 굳이 AWS에서 적극적으로 지원하는 운영체제를 선택하지 않을 이유가 없습니다.

다음은 인스턴스 유형을 선택하는 단계입니다.   
프리티어로 표기된 t2.micro를 선택합니다.   
![5](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/5.PNG)

여기서 t2는 요금 타입을 의미하며, micro는 사양을 이야기합니다.   
t2 외에 t3도 있으며 보통 이들을 T 시리즈라고 합니다.   
T 시리즈는 범용 시리즈로 불리기도 합니다.   
그만큼 다양한 사양을 사용할 수 있습니다.
> 다른 시리즈는 nano, micro 등의 저사양이 존재하지 않습니다.   

이들은 다른 서비스와 달리 크레딧이란 일종의 CPU를 사용할 수 있는 포인트 개념이 있습니다.   
인스턴스 크기에 따라 정해진 비율로 CPU 크레딧을 계속 받게 되며, 사용하지 않을 때는 크레딧을 축적하고, 사용할 때 이 크레딧을 사용합니다.   

정해진 사양보다 더 높은 트래픽이 오면 크레딧을 좀 더 적극적으로 사용하면서 트래픽을 처리하지만, 크레딧이 모두 사용되면 더이상 EC2를 사용할 수 없습니다.   
그래서 트래픽이 높은 서비스들은 T 시리즈를 쓰지 않고 다른 시리즈를 사용하기도 합니다.   
다만 활용도가 높기 때문에 시작하는 단계에서는 좋은 선택입니다.   

다음 단계는 세부정보 구성입니다.   
기업에서 사용할 경우 화면상에 표기된 VPC, 서브넷 등을 세세하게 다루지만, 지금은 혼자서 1대의 서버만 사용하니 별다른 설정을 하지 않고 넘어갑니다.   
> VPC와 서브넷 등은 AWS 서비스들의 네트워크 환경을 구성하는 정도로만 이해하면 됩니다.   

![6](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/6.PNG)

다음 단계는 스토리지 선택입니다.   
스토리지는 흔히 하드디스크라고 부르는 서버의 디스크(SSD도 포함)를 이야기하며 서버의 용량을 얼마나 정할지 선택하는 단계입니다.   

여기서 설정의 기본값은 8GB(기가바이트) 입니다.   
30GB까지 프리티어로 가능합니다.   
**그 이상의 사이즈는 비용이 청구되니** 프리티어의 최대치인 30GB로 변경합니다.    
![7](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/7.PNG)

태그에는 웹 콘솔에서 표기될 태그인 Name 태그를 등록합니다.   
태그는 해당 인스턴스를 표현하는 여러 이름으로 사용될 수 있습니다.   
EC2의 이름을 붙인다고 생각하고 넣으면 됩니다.   

여러 인스턴스가 있을 경우 이를 태그별로 구분하면 검색이나 그룹 짓기 편하므로 여기서 본인 서비스의 인스턴스를 나타낼 수 있는 값으로 등록합니다.   
![8](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/8.PNG)

다음으로 보안 그룹입니다.   
보안 그룹은 방화벽을 이야기합니다.   
'서버로 80 포트 외에는 허용하지 않는다'는 역할을 하는 방화벽이 AWS에서는 보안 그룹으로 사용됩니다.   

기존에 생성된 보안 그룹이 없으므로 보안 그룹 이름엔 유의미한 이름으로 변경합니다.   
![9](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/9.PNG)    
이 보안그룹 부분이 굉장히 중요한 부분입니다.   
유형 항목에서 SSH이면서 포트 항목에서 22인 경우는 AWS EC2에 터미널로 접속할 때를 이야기합니다.   
pem 키가 없으면 접속이 안 되니 전체 오픈(0.0.0.0/0, ::/0)하는 경우를 종종 발견합니다.   
이렇게 되면 이후 파일 공유 디렉토리나 깃허브 등에 실수로 pem 키가 노출되는 순간 서버에서 가상화폐가 채굴되는 것을 볼 수 있습니다.   

보안은 언제나 높을수록 좋으니 pem 키 관리와 지정된 IP에서만 ssh 접속이 가능하도록 구성하는 것이 안전합니다.   
그래서 본인 집의 IP를 기본적으로 추가하고(내 IP를 선택하면 현재 접속한 장소의 IP가 자동 지정됩니다) 카페와 같이 집 외에 다른 장소에서 접속할 때는 해당 장소의 IP를 다시 SSH 규칙에 추가하는 것이 안전합니다.   

현재 프로젝트의 기본 포트인 8080을 추가하고 [검토 및 시작] 버튼을 클릭합니다.   
검토 화면에서 보안 그룹 경고를 하는데, 이는 8080이 전체 오픈이 되어서 발생합니다.   
8080을 열어 놓은 것은 위험한 일이 아니니 바로 [시작하기] 버튼을 클릭합니다.   
![10](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/10.PNG)

인스턴스로 접근하기 위해서는 pem 키(비밀키)가 필요합니다.   
그래서 인스턴스 마지막 단계는 할당할 pem 키를 선택하는 것입니다.   

인스턴스는 지정된 pem 키(비밀키)와 매칭되는 공개키를 가지고 있어, 해당 pem 키 외에는 접근을 허용하지 않습니다.   

일종의 마스터키이기 때문에 절대 유출되면 안 됩니다.   
pem 키는 이후 EC2 서버로 접속할 때 필수 파일이니 **잘 관리할수 있는 디렉토리로 저장**합니다.   
기존에 생성된 pem 키가 있다면 선택하고 없다면 신규로 생성합니다.   
![11](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/11.PNG)

pem 키까지 내려받았다면 다음과 같이 인스턴스 생성 시작 페이지로 이동하고 인스턴스 id를 클릭하여 EC2 목록으로 이동합니다.   
![12](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/12.PNG)

인스턴스가 생성된 것을 확인할 수 있으며 Name 태그로 인해 Name이 노출되는 것도 확인 가능합니다.
![13](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/13.PNG)   

다음과 같이 IP와 도메인이 할당된 것을 확인할 수 있습니다.   
![14](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/14.PNG)   

인스턴스도 결국 하나의 서버이기 때문에 IP가 존재합니다.   
인스턴스 생성 시에 항상 새 IP를 할당하는데, 한 가지 조건이 있습니다.   
같은 인스턴스를 중지하고 다시 시작할때도 새 IP가 할당됩니다.   

즉, 요금을 아끼기 위해 잠깐 인스턴스를 중지하고 다시 시작하면 IP가 변경되는 것입니다.   
이렇게 되면 매번 접속해야 하는 IP가 변경돼서 PC에서 접근할 때마다 IP 주소를 확인해야 합니다.   
굉장히 번거로우므로 인스턴스의 IP가 매번 변경되지 않고 고정 IP를 가지게 해야 합니다.   
그래서 고정 IP를 할당하겠습니다.   

## EIP 할당
AWS의 고정 IP를 Elastic IP(EIP, 탄력적 IP)라고 합니다.   
EC2 인스턴스 페이지의 왼쪽 카테고리에서 탄력적 IP를 눌러 선택하고 주소가 없으므로 [탄력적 IP 주소 할당] 버튼을 클릭합니다.   
![15](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/15.PNG)

바로 [할당] 버튼을 클릭합니다.   
![16](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/16.PNG)

새 주소 할당이 완료되면 탄력적 IP가 발급됩니다.   
![17](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/17.PNG)

방금 생성한 탄력적 IP와 방금 생성한 EC2 주소를 연결합니다.   
방금 생성한 탄력적 IP를 확인하고, 페이지 위에 있는 [작업] 버튼 => [탄력적 IP 주소 연결] 메뉴를 선택합니다.   
![18](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/18.PNG)

주소 연결을 위해 생성한 EC2 이름과 IP를 선택하고 [연결] 버튼을 클릭합니다.   
![19](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/19.PNG)   

연결이 완료되면 왼쪽 카테고리에 있는 [인스턴스] 탭을 클릭해서 다시 인스턴스 목록 페이지로 이동합니다.   
![20](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/20.PNG)   

해당 인스턴스의 퍼블릭, 탄력적 IP가 모두 잘 연결되었는지 확인합니다.   
![21](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BEC2%5D%20AWS%20%EC%84%9C%EB%B2%84%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%202%20-%20EC2%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/21.PNG)

여기까지 진행했으면 EC2 인스턴스 생성 과정은 끝났습니다!   
하지만, 주의할 점이 있습니다.   
방금 생성한 탄력적 IP는 **생성하고 EC2 서버에 연결하지 않으면 비용이 발생합니다.**   
즉, **생성한 탄력적 IP는 무조건 EC2에 바로 연결해야 하며 만약 더는 사용할 인스턴스가 없을 때도 탄력적 IP를 삭제해야 합니다.**   
마찬가지로 비용 청구가 되므로 꼭 잊지 않고 삭제해야 합니다.   

## 참고
* [이동욱님의 스프링 부트와 AWS로 혼자 구현하는 웹 서비스](https://jojoldu.tistory.com/463)