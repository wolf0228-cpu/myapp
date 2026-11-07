# 🐳 Docker를 이용한 웹 서버 구축 및 배포 실습

본 프로젝트는 Nginx를 기반으로 커스텀 웹 페이지를 제작하고, Docker 컨테이너 기술을 활용하여 로컬 실행 및 클라우드 저장소(GitHub, Docker Hub)에 배포하는 과정을 수행한 결과물입니다.

## 1. 실습 환경
- **OS**: Windows 11
- **Docker**: Docker Desktop 27.2.0
- **Git**: Git 2.46.0
- **IDE**: Visual Studio Code

## 2. 프로젝트 구성 파일
- `index.html`: 사용자 정보(이상오 / 학번)와 스타일이 적용된 메인 페이지
- `Dockerfile`: Nginx 베이스 이미지를 활용한 이미지 빌드 설정 파일
- `.gitignore`: 불필요한 설정 파일 및 폴더 제외 설정
- `images/`: 실습 결과 캡처 이미지 저장 폴더

## 3. 웹 페이지 및 Dockerfile 상세
- **index.html**: 배경색 지정 및 CSS 스타일을 적용하여 가독성을 높인 웹 페이지 제작
- **Dockerfile**: 
  ```dockerfile
  FROM nginx:latest
  COPY index.html /usr/share/nginx/html/index.html