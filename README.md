# 🚀 개발 워크스테이션 구축 및 웹 서버 배포 프로젝트

## 1. 프로젝트 개요
- **목표**: Docker를 이용한 Nginx 웹 서버 구축, 커스텀 이미지 생성 및 GitHub/Docker Hub 배포.
- **성과**: 컨테이너 기술의 기초를 습득하고, 환경에 구애받지 않는 배포 파이프라인 구축 완료.

## 2. 실행 환경
- **운영체제**: Windows 11 (WSL2)
- **Terminal**: PowerShell / VSCode Terminal
- **Docker 버전**: 27.2.0
- **Git 버전**: 2.46.0

## 3. 수행 항목 체크리스트
- [x] Docker Desktop 설치 및 환경 설정
- [x] Nginx 베이스 Dockerfile 작성
- [x] 포트 매핑 (8080:80) 설정 및 접속 확인
- [x] Docker Hub 이미지 Push 성공 (`wolf02284075/my-web-app`)
- [x] GitHub 저장소 연동 및 소스 관리
- [x] 프로젝트 증빙용 스크린샷 정리 (`/images` 폴더)

## 4. 터미널 운영 로그 (핵심 명령)
```bash
# 이미지 빌드
docker build -t wolf02284075/my-web-app:latest .

# 컨테이너 실행 (포트 8080 연결)
docker run -d -p 8080:80 --name my-web-container wolf02284075/my-web-app:latest

# Docker Hub 배포
docker push wolf02284075/my-web-app:latest