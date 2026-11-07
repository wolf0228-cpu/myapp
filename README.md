# 🐳 Docker를 이용한 Nginx 웹 서버 구축 과제

## 1. 프로젝트 개요
- **작성자**: 이상오 (학번: 00000000)
- **목표**: Docker를 사용하여 Nginx 웹 서버를 구축하고, GitHub 및 Docker Hub에 배포한다.

## 2. 개발 환경
- **OS**: Windows 11
- **Tool**: Docker Desktop, VS Code, Git
- **Base Image**: nginx:latest

## 3. 주요 수행 내용
- [x] `index.html` 작성 (이름, 학번, 배경색 포함)
- [x] `Dockerfile` 작성 및 이미지 빌드
- [x] Docker 컨테이너 실행 및 포트 포워딩 (8080:80)
- [x] GitHub 원격 저장소 생성 및 소스 코드 푸시 (총 9회 커밋)
- [x] Docker Hub 이미지 푸시 (`wolf02284075/my-web-app:latest`)

## 4. 문제 해결 및 트러블슈팅
- **문제**: Dockerfile 파일명이 한글(`도커파일`)로 되어 있어 빌드 시 인식이 안 되는 문제 발생.
- **해결**: 파일명을 영문 `Dockerfile`로 수정하여 표준 규격을 맞춤.
- **문제**: GitHub 푸시 중 충돌 발생.
- **해결**: 로컬과 원격 저장소의 상태를 동기화한 후 다시 푸시하여 해결.

## 5. 실행 방법
```bash
# Docker Hub에서 이미지 다운로드
docker pull wolf02284075/my-web-app:latest

# 컨테이너 실행
docker run -d -p 8080:80 --name my-web-server wolf02284075/my-web-app:latest
## 6. 실습결과(이미지)
![alt text](<images/Docker Hub 업로드 화면 (docker_hub.png).png>)
![alt text](<images/GitHub 저장소 화면 (github_repo.png).png>)
![alt text](<images/도커 실행 확인 화면 (docker_ps.png).png>)
![alt text](<images/웹 브라우저 접속 화면 (web_result.png).png>)