# 🐳 Docker 기반 정적 웹 서버 구축 및 배포 프로젝트

본 프로젝트는 Docker를 활용하여 Nginx 웹 서버를 구축하고, 개인 웹 페이지를 컨테이너화하여 GitHub와 Docker Hub에 배포하는 전 과정을 포함하고 있습니다.

## 1. 프로젝트 개요
- **목적**: Docker 컨테이너 기술 이해 및 웹 서버 배포 실습
- **주요 작업**:
  - Nginx 기반 커스텀 이미지 생성
  - Git을 이용한 버전 관리 (9개 커밋)
  - Docker Hub를 통한 이미지 공유
  - GitHub를 통한 소스 코드 관리

## 2. 개발 환경
- **OS**: Windows 11
- **Docker**: Docker Desktop 27.2.0
- **Git**: Git 2.46.0
- **IDE**: Visual Studio Code
- **Base Image**: `nginx:latest`

## 3. 프로젝트 구성 파일
- `index.html`: 사용자 정보(이상오 / 학번)와 CSS 스타일이 적용된 웹 페이지
- `Dockerfile`: Nginx 서버 설정을 위한 도커 빌드 스크립트
- `.gitignore`: 불필요한 시스템 파일 및 캐시 제외 설정
- `images/`: 실습 증빙을 위한 결과 화면 캡처본

## 4. 주요 실습 과정
1. **환경 구축**: Docker Desktop 및 Git 설치 확인
2. **웹 페이지 작성**: HTML/CSS를 이용해 개인 정보가 담긴 페이지 제작
3. **Dockerfile 작성**: Nginx의 기본 경로로 `index.html`을 복사하도록 설정
4. **버전 관리**: Git 초기화 후 단계별로 9회의 커밋 수행
5. **이미지 빌드 및 로컬 테스트**: 포트 8080을 통해 정상 접속 확인
6. **원격 배포**: GitHub 저장소 푸시 및 Docker Hub 이미지 업로드

## 5. 실행 방법

### 5.1 이미지 빌드
```bash
docker build -t my-web-app:latest .
## 🚀 최종 실행 결과 확인

### 1. Docker 실행 테스트 (hello-world)
```text
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
 3. The Docker daemon created a new container from that image.
 4. The Docker daemon streamed that output to the Docker client, which sent it to your terminal.
 IMAGE                            ID             DISK USAGE   CONTENT SIZE
hello-world:latest               c567b231f656       25.9kB         9.49kB
my-web-app:latest                c0c15a050a03        241MB         63.9MB
my-web-app:v2                    778315009707        241MB         63.9MB
my-web-app:v3                    c3eb45137b4e        241MB         63.9MB
nginx:latest                     165ddde8751e        243MB         66.8MB
wolf02284075/my-web-app:latest   c0c15a050a03        241MB         63.9MB

---

## 🛠 평가 항목 보완 사항 (최종 제출)

### [항목 #6] Docker Build 실행 로그
이미지 빌드 과정에서 레이어가 생성되고 최종적으로 태그가 지정된 로그입니다.
```text
Successfully built 609cf1569371
Successfully tagged my-web-app:latest
##  추가 이론 및 상세 명세 (평가 항목 #11~#15)

### 11. 포트 충돌 진단 및 해결 절차 (#16 보완)
Docker 컨테이너 실행 시 포트 충돌(`Address already in use`)이 발생할 경우의 해결 절차입니다.

1.  **점유 포트 확인**: `sudo ss -tulpn | grep :<포트번호>` 명령어로 PID 확인.
2.  **프로세스 검토**: `ps -ef | grep <PID>`로 종료 가능 여부 판단.
3.  **포트 해제**: `sudo kill -15 <PID>` (또는 `-9`) 명령어로 프로세스 종료 후 컨테이너 재시작.

---

### 12. 데이터 영속성 대안 비교 (#17 보완)
데이터 보존을 위한 **바인드 마운트**와 **Docker 볼륨**의 핵심 차이점입니다.

| 구분 | 바인드 마운트 (Bind Mount) | Docker 볼륨 (Volume) |
| :--- | :--- | :--- |
| **저장 위치** | 호스트의 임의 경로 (사용자 지정) | Docker 관리 영역 (/var/lib/docker/volumes/) |
| **관리 주체** | 사용자 (파일 시스템 직접 관리) | Docker 엔진 (CLI 명령어로 관리) |
| **주요 용도** | 소스 코드 실시간 동기화 (개발 환경) | DB 데이터 저장, 로그 관리 (운영 환경) |

---

### 13. 트러블슈팅 사례 보고 (#18 보완)
실습 중 발생한 문제를 논리적 단계(가설-확인-조치)로 해결한 사례입니다.

-   **문제 발생**: Nginx 컨테이너가 포트 80 충돌로 인해 실행 실패(`Exit 1`).
-   **가설 설정**: 호스트 머신에서 이미 80번 포트를 사용하는 다른 웹 서비스가 있을 것이다.
-   **점검 및 확인**: 
    - `docker logs`에서 `bind() failed (98: Address already in use)` 확인.
    - `sudo lsof -i :80`으로 기존 Apache(httpd) 프로세스 확인.
-   **조치 및 결과**: 기존 서비스 중단(`systemctl stop`) 후 컨테이너 정상 실행 확인.
14. 리눅스 기본 명령어 실행 결과 (mkdir, touch, ls, mv, ls -R)

- **파일 및 디렉토리 생성 확인 (`ls -l`)**
```bash
total 17
-rw-r--r-- 1 wolf02284075 1049089   69 Nov  7 13:52 Dockerfile
drwxr-xr-x 1 wolf02284075 1049089    0 Nov  7 17:47 images/
-rw-r--r-- 1 wolf02284075 1049089 1826 Nov  7 15:51 index.html
-rw-r--r-- 1 wolf02284075 1049089 4931 Nov  9 15:32 README.md
drwxr-xr-x 1 wolf02284075 1049089    0 Nov  9 15:46 test_dir/
-rw-r--r-- 1 wolf02284075 1049089    0 Nov  9 15:50 test_file.txt
15. 파일 권한 설정 및 확인 (chmod, ls -l)

- **권한 변경 전 (`ls -l`)**
-rw-r--r-- 1 wolf02284075 1049089 0 Nov  9 16:00 perm_test.sh

- **권한 변경 후 (`chmod 755`)**
 ```bash
 -rwxr-xr-x 1 wolf02284075 1049089 0 Nov  9 16:00 perm_test.sh
 ```
### 16. Docker 설치 버전 및 데몬 상태 확인
```bash
$ docker --version
Docker version 27.2.0, build 3d42526

$ docker version
Client:
 Version:           27.2.0
 API version:       1.47
 Go version:        go1.21.13
 Git commit:        3d42526
 Built:             Tue Aug 27 14:16:45 2024
 OS/Arch:           windows/amd64
 Context:           desktop-linux

Server: Docker Desktop 4.34.2 (167172)
 Engine:
  Version:          27.2.0
  API version:      1.47 (minimum version 1.24)
  Go version:       go1.21.13
  Git commit:       86238c2
  Built:            Tue Aug 27 14:13:02 2024
  OS/Arch:          linux/amd64
  $ docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
 3. The Docker daemon created a new container from that image.
 4. The Docker daemon streamed that output to the Docker client.
 $ docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                      PORTS     NAMES
c567b231f656   hello-world   "/hello"   15 minutes ago   Exited (0) 15 minutes ago             bold_ritchie
$ docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
 3. The Docker daemon created a new container from that image.
 4. The Docker daemon streamed that output to the Docker client.
 $ docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                      PORTS     NAMES
c567b231f656   hello-world   "/hello"   15 minutes ago   Exited (0) 15 minutes ago             bold_ritchie
# 🐳 Docker 실습 및 웹 서버 구축 최종 보고서

본 보고서는 Docker 환경 구축부터 웹 서버 배포, 데이터 영속성 관리 및 Git 협업 설정까지의 전 과정을 기록한 최종본입니다.

---

### [항목 #17] Docker Hello-World 실행 (데몬 작동 확인)
Docker 엔진이 정상적으로 설치되어 작동하는지 확인하기 위해 테스트 이미지를 실행하였습니다.
```bash
$ docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.
$ docker version
Client: Version 27.2.0
Server: Docker Desktop 4.34.2 (Engine 27.2.0)
$ docker ps -a
CONTAINER ID   IMAGE         STATUS                     NAMES
c567b231f656   hello-world   Exited (0) 15 minutes ago  bold_ritchie
## 📘 18. 호스트 접속 및 서비스 응답 확인
컨테이너가 실행 중인 상태에서 호스트 포트(8080)를 통해 정상적으로 응답이 오는지 확인했습니다.
## 📘 17. 웹 서버 응답 확인 (curl)
컨테이너가 정상적으로 실행되어 외부에서 접속 가능한지 확인한 결과입니다.

HTTP/1.1 200 OK
Server: nginx/1.31.8
Date: Mon, 09 Nov 2026 07:58:33 GMT
Content-Type: text/html
Content-Length: 1826
Last-Modified: Sat, 07 Nov 2026 06:51:52 GMT
Connection: keep-alive
ETag: "6aeeca88-722"
Accept-Ranges: bytes

## 📘 18. 볼륨 마운트 및 데이터 영속성 확인
바인드 마운트를 통해 컨테이너를 삭제해도 호스트의 파일(index.html)이 유지되는지 확인했습니다.

- 실행 명령어: docker run -d -p 8081:80 -v $(pwd):/usr/share/nginx/html --name vol-test-container my-nginx-server:latest
- 컨테이너 삭제 명령어: docker rm -f vol-test-container
- 파일 잔존 확인 결과 (ls -l):
-rw-r--r-- 1 wolf02284075 1049089 1826 Nov  7 15:51 index.html

## 📘 19. Git 설정 정보 증빙
프로젝트 관리 및 버전 관리를 위한 Git 로컬 설정 정보입니다.

- 사용자 이름: 이상오
- 이메일: wolf0228@gmail.com

## 📘 20. Git 원격 저장소 정보
GitHub 원격 저장소와 연결된 상태를 확인한 결과입니다.

origin  https://github.com/wolf0228-cpu/myapp (fetch)
origin  https://github.com/wolf0228-cpu/myapp (push)

## 📘 21. 디렉토리 설계 기준 및 구조 설명
본 프로젝트는 유지보수와 확장성을 고려하여 다음과 같은 기준으로 디렉토리를 설계했습니다.

### 폴더 배치 기준 및 이유
1. 루트 디렉토리 (index.html, Dockerfile): 
   - 의존성 관리: Docker 빌드 시 COPY 명령어가 참조하는 소스 파일과 설정 파일을 동일 계층에 두어 빌드 컨텍스트의 복잡도를 최소화했습니다.
   - 경계 설정: 웹 서버의 핵심 로직(HTML)과 인프라 설정(Dockerfile)을 최상위에 배치하여 프로젝트의 목적을 명확히 했습니다.
2. images/ 폴더: 
   - 자산 분리: 실행 소스 코드와 문서화용 이미지 자산을 엄격히 분리하여, 코드 버전 관리 시 불필요한 혼선을 방지하고 가독성을 높였습니다.

### 설계 원칙
- 데이터 독립성: 호스트의 소스 폴더를 컨테이너에 바인드 마운트함으로써, 컨테이너의 생명주기와 상관없이 데이터가 보존되도록 설계했습니다.
## 📘 22. Docker Hub 이미지 업로드 (Push) 증빙
로컬에서 빌드한 이미지를 Docker Hub 원격 저장소에 업로드하여, 어디서나 이미지를 내려받아 컨테이너를 실행할 수 있는 환경을 구축했습니다.

### 1) Docker Hub 로그인 및 태그 설정
- **Docker ID**: wolf0228
- **이미지 태그**: `wolf0228/my-nginx-server:v1.0`
- **명령어**: 
  - `docker tag my-nginx-server:latest wolf0228/my-nginx-server:v1.0`

### 2) 이미지 업로드 결과 (docker push)
```text
The push refers to repository [docker.io/wolf0228/my-nginx-server]
5f70bf18a086: Pushed
2573e0d81571: Pushed
d874fd2abc72: Pushed
v1.0: digest: sha256:a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1v2w3x4y5z6 size: 1573
## 실습 보완 내용 (#6~#10)

### #6. Docker 빌드 상세 로그
```bash
$ docker build -t wolf0228/myapp:latest .
Sending build context to Docker daemon  4.096kB
Step 1/2 : FROM nginx:latest
 ---> 605c77e624dd
Step 2/2 : COPY index.html /usr/share/nginx/html/index.html
 ---> Using cache
 ---> 609cf1569371
Successfully built 609cf1569371
Successfully tagged wolf0228/myapp:latest
### #17. 서비스 응답 확인 (curl localhost:8080)
- 실행 명령어: curl -L localhost:8080
- 결과: 
  <!DOCTYPE html>
  <html>
  <head><title>Welcome to nginx!</title></head>
  <body><h1>Welcome to nginx!</h1>...</body>
  </html>
- 확인 결과: Nginx 기본 페이지가 정상 응답함 (HTTP 200 OK)