# 🐳 Docker 웹 서버 구축 및 GitHub 배포 미션

> **작성자:** 이상오  
> **상태:** ✅ 미션 완료  
> **최종 업데이트:** 2024-11-07

---

## 💻 1. 실행 환경 (Environment)

| 구분 | 상세 내용 |
| :--- | :--- |
| **OS** | Windows 11 (Docker Desktop) |
| **Docker** | Docker Engine 24.x 이상 |
| **Git** | Git for Windows 2.x 이상 |
| **Base Image** | `nginx:latest` |

---

## 📑 2. 수행 체크리스트 (Checklist)

- [x] **Dockerfile 작성:** Nginx 기반의 커스텀 이미지 설계
- [x] **이미지 빌드:** `docker build`를 통한 로컬 이미지 생성
- [x] **컨테이너 실행:** 포트 포워딩(`8080:80`) 설정 및 구동
- [x] **권한 실습:** Linux 권한(`chmod`) 변경 및 확인
- [x] **GitHub 연동:** 원격 저장소 푸시 및 README 작성

---

## 🛠️ 3. 주요 수행 로그 (Evidence)

### 🔓 권한 변경 실습 (Permission Test)
`ubuntu` 컨테이너 환경에서 파일 생성 및 권한 변경을 수행한 결과입니다.

```bash
# 명령어 실행 결과
-rw-r--r-- 1 root root 0 Nov 7 06:00 test.txt  <-- 초기 상태
-rwxrwxrwx 1 root root 0 Nov 7 06:00 test.txt  <-- chmod 777 적용 후