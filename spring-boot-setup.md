## Spring Boot 배포하기 (2024.12.15)

### 1. Spring Boot 배포 파일 준비  
1. 터미널에서 명령어 입력한다  
```cmd
 mvn clean package
```
2. target 경로에 jar 배포 파일이 생성됨
![image](https://github.com/user-attachments/assets/791ff0d5-fc8b-418d-b84e-c220695daa07)

3. 생성된 jar 파일을 대상 서버로 옮기고 java로 실행해본다
> 오류가 발생하는지 확인해보는 과정

### 2. Spring Boot 서비스로 실행되도록 설정
1. javaSpring.service 생성
- 만약 Error로그를 쌓고 싶으면 standardError에 Error.log파일 경로를 넣으면 됨
```
[Unit]
Description=Spring Boot Application
After=network.target

[Service]
User=실행할 계정
ExecStart=(자바 설치 경로) -jar (배포할 jar파일 경로)
WorkingDirectory=/usr/share/javaSpring
SuccessExitStatus=143
Restart=always
RestartSec=10
StandardOutput=null
StandardError=null

[Install]
WantedBy=multi-user.target
```
2. 서비스를 실행한다
```cmd
sudo systemctl restart javaSpring.service
```

### 3. 도메인과 연결 (선택 사항)
- Nginx 에 설정을 추가
- 내 프로젝트는 8080포트로 실행되도록 하여 8080으로 설정하였다.
```
server {
    listen 8080;
    server_name 설정 도메인;
}
```
정상 적용 확인  
![image](https://github.com/user-attachments/assets/8571ed65-27eb-473e-8574-b90494c24e45)
