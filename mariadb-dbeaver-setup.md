## MariaDB 설치 및 DBeaver연결 (2023.07.29)

### 1. MariaDB을 서버에 설치/ MariaDB 접근 권한이 있는 계정을 생성  
<a id="mariadb-setup"></a>

- 참고 : https://marsland.tistory.com/510

### 2. DB 연결을 할 수 있는 3306포트 방화벽 오픈

- 참고 : https://myjamong.tistory.com/7﻿

### 3. DBeaver 연결
- DBeaver을 다운 https://dbeaver.io/download/﻿
- ssh 활용하여 서버 연결  
네이버 클라우드에 3306 포트도 포트포워딩하려 했지만 UI 구성 상 하나만 열 수 있는 것 같다. ( 아닐 수 있음 )

우선 개발 환경 세팅은 ssh 연결을 이용하여 DBeaver에 연결해보려 한다

1. ssh에 "Use SSH 터널"을 체크하고 연결하려는 서버 IP를 입력하고 포트포워딩된 포트를 입력
2. 아이디 비번은 서버 접근용 계정으로 입력
3. 하단에 Test Connection으로 ssh연결이 되는지 확인 가능

![image](https://github.com/user-attachments/assets/091a8765-332a-4064-ac7a-d5b8166d2c78)


1. main으로 이동 후 server Host에 localhost, port를 3306으로 입력
2. 아이디 비번은 MariaDB 접근 권한이 있는 계정으로 입력 [1번 참고 링크 확인](#mariadb-setup)
> ssh 연결로 할 경우 main에 데이터베이스 3306 연결하는 부분은 연결할 서버 ip가 아닌 localhost로 해야한다  
> 'ssh 접속 -> localhost 3306 포트로 접속 -> 연결' 이런 개념으로 이해 중이다

![image](https://github.com/user-attachments/assets/56d96a7e-2141-4193-b0ca-c5a6e43a6e63)

- 참고 : https://nufyn.tistory.com/entry/DBeaver-설치-및-원격-MariaDB-SSH-연결Mac﻿
