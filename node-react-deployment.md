## Node 배포하기, 리액트와 연결하기 (2024.09.18)

### 1. Node 설치

- 참고 : https://nirsa.tistory.com/193

### 2. React 배포 파일 준비
FileZille를 이용해 배포할 것이다.  
아래 명령어 실행 후 build 파일안에 소스를 배포하면 된다.
```cmd
npm run build
```

### 3. Node 배포 및 서비스 화
3-1. package.json, 실행될 node 파일 반입  
3-2. 배포 폴더 내에서 모듈 설치 진행  
```cmd
npm install
```
3-3. 테스트로 node ~ 명령어 실행하여 오류 발생하는지 확인  
```cmd
node server.js
```
3-4. pm2 활용하여 터미널 종료 후에도 실행되도록 설정  
- pm2 설치
```cmd
npm install pm2 -g
```
- pm2으로 배포한 node 파일 실행
```cmd
pm2 start server.js
pm2 startup
```

### 4. React를 NGINX에 연동

- 참고 : https://catnails.tistory.com/423#google_vignette

### 5. CORS 정책 설정
5-1. NGINX 설정 파일 열기
```cmd
sudo nano /etc/nginx/conf.d/default.conf
```
5-2. /api/~ 으로 접근을 허용하는 설정 추가
```
server {
    listen 80;
    
    location / {
        root /usr/local/front-app;
        index index.html index.htm;
        try_files $uri $uri/ /index.htm;
    }

    location /api/ {
        add_header 'Access-Control-Allow-Origin' '*';
        add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS, DELETE, PUT';
        add_header 'Access-Control-Allow-Headers' 'Content-Type, Authorization';

        if ($request_method = 'OPTIONS') {
            add_header 'Access-Control-Allow-Origin' '*';
            add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS, DELETE, PUT';
            add_header 'Access-Control-Allow-Headers' 'Content-Type, Authorization';
            return 204;
        }
    }
}
```
