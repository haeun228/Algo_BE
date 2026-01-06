# ALGO Backend

**알고리즘 문제 풀이 기록 서비스 ALGO**의 백엔드 레포지토리입니다.  
사용자는 문제 풀이 과정을 기록하고, 복습·통계·스트릭 관리 기능을 통해 학습을 지속할 수 있습니다.

<br>

## 📌 주요 기능

- **소셜 로그인 기반 사용자 인증** : Google / Kakao / GitHub OAuth를 통한 간편 로그인 지원

- **알고리즘 문제 자동 조회** : 외부 알고리즘 플랫폼 문제 URL 기반 정보 자동 수집

- **문제 풀이 기록 관리** : 풀이 상태, 난이도, 메모를 포함한 기록 생성 및 수정

- **풀이 과정 구조화** : 단계별 풀이 과정과 코드 스니펫 분리 저장

- **복습 및 학습 관리** : 복습 이력 관리 및 추천 복습 문제 제공

- **스트릭 및 통계 제공** : 연속 학습 스트릭과 일별 학습 통계 시각화

- **북마크 및 유형 분류** : 중요한 기록 저장 및 문제 유형 기반 분류

<br>

## 🛠️ 기술 스택
| 분류 | 사용 기술 |
|----|----|
| Language | Java |
| Framework | Spring Boot |
| Database | MySQL |
| ORM | Spring Data JPA (Hibernate) |
| Authentication | OAuth 2.0 (Google / Kakao / GitHub) |
| Build Tool | Gradle |
| API Style | RESTful API |

<br>

## 🗂️ ERD

프로젝트는 사용자, 문제, 기록, 복습, 통계 도메인을 중심으로 설계되었습니다.

![ERD](https://github.com/user-attachments/assets/a51314cc-bbde-4131-8e9a-f1cc663be37e)

- **`User`** : OAuth 기반 사용자 정보와 학습 활동(기록, 복습, 통계, 스트릭)의 기준이 되는 엔티티
- **`Problem`** : 외부 알고리즘 플랫폼의 문제 정보를 관리하며 기록에서 공통으로 참조
- **`Record`** : 사용자의 알고리즘 문제 풀이 기록을 관리하는 핵심 엔티티
- **`RecordStep`** : 문제 풀이 과정을 단계별로 저장하여 사고 흐름을 정리
- **`RecordCode`** : 문제 풀이에 사용된 코드 스니펫과 실행 결과를 관리
- **`Category`** : 문제 유형 분류를 위한 엔티티로 기록과 다대다 관계
- **`Bookmark`** : 사용자가 저장한 문제 기록 관리
- **`ReviewLog`** : 문제 복습 이력을 관리하여 복습 추천 및 완료 처리에 활용
- **`StatsDaily`** : 사용자 일별 학습 통계를 저장하여 대시보드에 활용

<br>

## 🔗 주요 API

서비스의 핵심 기능과 관련된 주요 API 목록입니다.

| 분류 | 메서드 | 경로 | 설명 |
|----|----|----|----|
| 📝 문제 기록 | GET | `/api/records` | 문제 풀이 기록 목록 조회 |
|  | POST | `/api/records` | 문제 풀이 기록 생성 |
|  | GET | `/api/records/{recordId}` | 문제 풀이 기록 상세 조회 |
|  | PUT | `/api/records/{recordId}` | 문제 풀이 기록 수정 |
|  | DELETE | `/api/records/{recordId}` | 문제 풀이 기록 삭제 |
| 🧩 문제 | GET | `/api/problems/fetch` | 외부 알고리즘 문제 정보 자동 조회 |
| ⭐ 북마크 | POST | `/api/bookmarks/{recordId}` | 기록 북마크 등록 |
|  | DELETE | `/api/bookmarks/{recordId}` | 기록 북마크 해제 |
| 🔁 복습 | GET | `/api/users/me/reviews` | 복습 대상 문제 조회 |
|  | POST | `/api/users/me/reviews/{recordId}` | 복습 완료 처리 |
| 📊 통계 | GET | `/api/users/me/stats` | 사용자 학습 통계 조회 |
|  | GET | `/api/users/me/streak` | 사용자 스트릭 조회 |
