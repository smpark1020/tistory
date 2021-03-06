## RDS 소개
이번에는 데이터베이스를 구축하고 앞 장에서 만든 EC2 서버와 연동을 해보겠습니다.   
직접 데이터베이스를 설치해서 다루게 되면 모니터링, 알람, 백업, HA 구성 등을 모두 직접 해야만 합니다.   
처음 구축할 때 며칠이 걸릴 수 있는 일입니다.   

AWS에서는 앞에 언급한 작업을 모두 지원하는 관리형 서비스인 RDS(Relational Database Service)를 제공합니다.   
RDS는 AWS에서 지원하는 클라우드 기반 관계형 데이터베이스입니다.   
하드웨어 프로비저닝, 데이터베이스 설정, 패치 및 백업과 같이 잦은 운영 작업을 자동화하여 개발자가 개발에 집중할 수 있게 지원하는 서비스입니다.   
추가로 조정 가능한 용량을 지원하여 예상치 못한 양의 데이터가 쌓여도 비용만 추가로 내면 정상적으로 서비스가 가능한 장점도 있습니다.   

## RDS 인스턴스 생성하기
먼저 RDS 인스턴스를 생성하겠습니다.   
다음과 같이 검색창에 rds를 입력해서 선택하고, RDS 대시보드에서 [데이터베이스 생성] 버튼을 클릭합니다.   
![1](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BRDS%5D%20AWS%EC%97%90%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%201%20-%20RDS%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/1.PNG)   
![2](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BRDS%5D%20AWS%EC%97%90%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%201%20-%20RDS%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/2.PNG)   

RDS 생성 과정이 진행됩니다.   
DB 엔진 선택 화면에서 MariaDB를 선택하도록 하겠습니다.   
RDS에는 오라클, MSSQL, PostgreSQL 등이 있으며 당연히 본인이 가장 잘 사용하는 데이터베이스를 고르면 되지만, 꼭 다른 데이터베이스를 선택해야 하는 이유가 아니라면 MySQL, MariaDB, PostgreSQL 중에 고르길 추천합니다.   

MariaDB를 추천하는 이유
* 가격
* Amazon Aurora(오로라) 교체 용이성

RDS의 가격은 라이센스 비용 영향을 받습니다.   
상용 데이터베이스인 오라클, MSSQL이 오픈소스인 MySQL, MariaDB, PostgreSQL 보다는 동일한 사양 대비 더 가격이 높습니다.   
결국 프리티어 기간인 1년이 지나면 비용을 지불하면서 RDS를 써야 합니다.   
비용 문제를 생각해 볼 필요가 있습니다.   

두 번째로 Amazon Aurora 교체 용이성입니다.   
Amazon Aurora는 AWS에서 MySQL과 PostgreSQL을 클라우드 기반에 맞게 재구성한 데이터베이스 입니다.    
공식 자료에 의하면 RDS MySQL 대비 5배, RDS PostgreSQL 보다 3배의 성능을 제공합니다.   
더군다나 AWS에 직접 엔지니어링하고 있기 때문에 계속해서 발전하고 있습니다.   
현재도 다른 데이터베이스와 비교해 다양한 기능을 제공하고 있습니다.   

클라우드 서비스에 가장 적합한 데이터베이스이기 때문에 많은 회사가 Amazon Aurora를 선택합니다.   
그러다 보니 호환 대상이 아닌 오라클, MSSQL을 굳이 선택할 필요가 없습니다.   
이렇게 보면 Aurora를 선택하면 가장 좋을 것 같지만 시작하는 단계에서 Aurora를 선택하기 어렵습니다.   
프리티어 대상이 아니며, 최저 비용이 월 10만 원 이상이기 때문에 부담스럽습니다.
그래서 MariaDB로 시작하겠습니다.   

국내외를 가리지 않고 오픈소스 데이터베이스 중 가장 인기 있는 제품을 고르라고 하면 MySQL을 꼽습니다.   
단순 쿼리 처리 성능이 어떤 제품보다 압도적이며 이미 오래 사용되어 왔기 때문에 성능과 신뢰성 등에서 꾸준히 개선되어 온 것도 장점입니다.   

발전하던 MySQL이 2010년에 썬마이크로시스템즈와 오라클이 합병되면서 많은 MySQL 개발자들은 썬마이크로시스템즈를 떠나며 본민만의 프로젝트를 진행하게 됩니다.   
이 중 MySQL의 창시자인 몬티 와이드니어가 만든 프로젝트가 MariaDB입니다.   

MySQL을 기반으로 만들어졌기 때문에 쿼리를 비롯한 전반적인 사용법은 MySQL과 유사하니 사용 방법에 대해서는 크게 걱정하지 않아도 됩니다.   
비슷한 사용법 외에도 MariaDB는 MySQL 대비 다음의 장점이 있습니다.   
* 동일 하드웨어 사양으로 MySQL보다 향상된 성능
* 좀 더 활설화된 커뮤니티
* 다양한 기능
* 다양한 스토리지 엔진

이제 다시 MariaDB를 선택하여 다음으로 이동합니다.   
![3](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BRDS%5D%20AWS%EC%97%90%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%201%20-%20RDS%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/3.PNG)   

다음으로 넘어가면 사용 사례 항목이 나옵니다.   
프리티어로 이용하려면 프리티어를 선택해야 하니 [프리티어]를 선택합니다.   
![4](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BRDS%5D%20AWS%EC%97%90%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%201%20-%20RDS%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/4.PNG)   

DB 인스턴스와 마스터 사용자 정보를 등록할 수 있습니다.   
![6](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BRDS%5D%20AWS%EC%97%90%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%201%20-%20RDS%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/6.PNG)

상세 설정에서는 다음 그림과 같은 설정을 합니다.   
![5](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BRDS%5D%20AWS%EC%97%90%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%201%20-%20RDS%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/5.PNG)

본인만의 DB 인스턴스 이름과 사용자 정보를 등록합니다.   
여기서 사용된 사용자 정보로 실제 데이터베이스에 접근하게 되니 어딘가 메모해 놓아도 좋습니다.   

네트워크에선 퍼블릭 엑세스를 [예]로 변경합니다.   
이후 보안 그룹에서 지정된 IP만 접근하도록 막을 예정입니다.   
![7](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BRDS%5D%20AWS%EC%97%90%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%201%20-%20RDS%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/7.PNG)   

데이터베이스 옵션에서는 이름을 제외한 나머지를 그림과 동일하게 하면 됩니다.   
파라미터 그룹의 변경을 이후에 진행할 예정이니 일단은 기본값으로 둡니다.   
![8](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BRDS%5D%20AWS%EC%97%90%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%201%20-%20RDS%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/8.PNG)   

모든 설정이 끝나서 [데이터베이스 생성] 버튼을 클릭하여 다음과 같이 생성 과정이 진행됩니다.    
![9](https://raw.githubusercontent.com/smpark1020/tistory/master/AWS/%5BRDS%5D%20AWS%EC%97%90%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%20%ED%99%98%EA%B2%BD%20%EB%A7%8C%EB%93%A4%EA%B8%B0%201%20-%20RDS%20%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0/9.PNG)   

## 참고
* [이동욱님의 스프링 부트와 AWS로 혼자 구현하는 웹 서비스](https://jojoldu.tistory.com/463)