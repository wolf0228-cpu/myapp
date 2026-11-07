# 🚀 개발 워크스테이션 구축 및 웹 서버 배포 프로젝트

## 1. 프로젝트 개요
- **목표**: Docker를 이용한 Nginx 웹 서버 구축, 커스텀 이미지 생성 및 GitHub/Docker Hub 배포.
- **성과**: 컨테이너 기술을 이해하고, 환경에 구애받지 않는 배포 파이프라인 구축.

## 2. 실행 환경
- **OS**: Windows 11 (WSL2)
- **Terminal**: PowerShell / VSCode Terminal
- **Docker Version**: 27.2.0 (또는 상오님 컴퓨터에서 `docker --version` 쳤을 때 나오는 값)
- **Git Version**: 2.46.0 (또는 `git --version` 값)

## 3. 수행 항목 체크리스트
- [x] Docker Desktop 설치 및 환경 설정
- [x] Nginx 베이스 Dockerfile 작성
- [x] 포트 매핑 (8080:80) 설정 및 접속 확인
- [x] Docker Hub 이미지 Push 성공
- [x] GitHub 저장소 연동 및 소스 관리
- [x] 바인드 마운트 및 볼륨 설정 검증

## 4. 터미널 운영 로그 (핵심 명령)
```bash
# 이미지 빌드
docker build -t wolf02284075/my-web-app:latest .

# 컨테이너 실행 및 포트 매핑
docker run -d -p 8080:80 --name my-web-container wolf02284075/my-web-app:latest

# 컨테이너 상태 확인
docker ps -a