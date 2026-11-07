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