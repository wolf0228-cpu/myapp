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