# PROGRESS — 진행 상황 (세이브 파일)

> 세션이 끊기면 Claude에게 **"PROGRESS.md 보고 튜토리얼 이어서 진행하자"** 라고 말하세요.
> 한 단계를 마칠 때마다 이 파일을 갱신합니다.

## 📍 현재 위치
- **Phase 0. 개발 환경 준비** — 거의 완료 (가이드: `docs/phases/phase0_개발환경.md`)
  - ✅ Step 1~4: 터미널, VS Code 확장, git init·.gitignore·첫 커밋(`9c61479`), PostgreSQL 19.0 설치·psql/pgAdmin 접속 확인
  - ⏳ Step 5: GitHub 비공개 저장소 연결 & push
- 마지막 업데이트: 2026-11-19

## ▶️ 다음 할 일
1. Phase 0 Step 5: GitHub 비공개 저장소 만들고 `git push -u origin main`
2. Step 6: `docs: Phase 0 완료` 커밋 & push
3. Phase 1 시작: **ERP 모듈 선정** 상의부터

## ✅ Phase 체크리스트
- [ ] Phase 0. 개발 환경 준비
- [ ] Phase 1. 주제 선정 & 기획
- [ ] Phase 2. 아키텍처 & 상세 설계
- [ ] Phase 3. Node.js 기초 워밍업
- [ ] Phase 4. erp-service (업무 API + DB)
- [ ] Phase 5. auth-service (회원가입·로그인·JWT)
- [ ] Phase 6. API Gateway
- [ ] Phase 7. React 클라이언트
- [ ] Phase 8. 권한(인가) & 보안 강화
- [ ] Phase 9. 테스트 & 로깅
- [ ] Phase 10. 배포 준비 (Linux · 운영 설정 · Docker)
- [ ] Phase 11. 클라우드 서버 3대로 분리 배포
- [ ] Phase 12. 백업 · 복구 · 장애 격리 훈련 & 회고

## 🧭 결정 기록
| 날짜 | 결정 | 이유 |
|---|---|---|
| 2026-11-14 | 언어: JavaScript (Node.js v24) | 사용자 요청 — JS로 전 과정 학습 |
| 2026-11-14 | 프론트엔드: 처음부터 React (Vite) | 사용자 선택 |
| 2026-11-14 | 백엔드: Express | 가볍고 동작 원리가 잘 보여 초보자에게 적합 |
| 2026-11-14 | DB: PostgreSQL, 서비스별 DB 분리(auth_db, erp_db) | 무료·강력, 서비스가 각자 데이터를 소유하는 구조 학습 |
| 2026-11-14 | 구성: gateway(8000) / auth-service(8001) / erp-service(8002) / web(5173) / PostgreSQL(5432) | 사용자가 원한 "게이트웨이 + 인증 + DB" 구조 |
| 2026-11-14 | 실행: 처음엔 로컬 직접 실행, Docker는 Phase 10 | PC가 Windows 10 1909로 Docker Desktop 설치가 어려울 수 있음 |
| 2026-11-14 | 보안(정규식 입력검증, SQL 인젝션 방어, 보안 설정)을 Phase 4부터 단계별로 적용 | 사용자 요청 — 로드맵의 "🛡️ 보안 원칙" 표 참고 |
| 2026-11-14 | 운영 시 **클라우드 서버 3대**(웹/게이트웨이 · 애플리케이션 · DB)로 물리 분리, **무료 범위 안에서** | 사용자 요청 — 장애 격리·보안 분리 경험. 사용자 PC: RAM 16GB, i5 4코어 (로컬 VM도 대안으로 가능) |
| 2026-11-14 | 서버 분리는 **설계는 Phase 2부터, 적용은 Phase 11** | 개발은 내 PC에서 하고 앱 완성 후 옮겨야 문제 원인 구분이 쉬움 |
| 2026-11-14 | 장애 대비 범위: **백업·복구 + 장애 격리 훈련** (이중화는 개념만) | 초보자에게 현실적인 범위 |
| 2026-11-19 | PostgreSQL **19.0** 설치 (포트 5432) | 설치 시점 최신 버전, 구버전 Windows에서도 정상 설치됨 |
| 2026-11-19 | GitHub **비공개(Private)** 원격 저장소 사용 | 코드 백업 + 다른 기기 열람. 비공개라도 비밀값은 올리지 않음 |

## 🤝 아직 상의할 항목 (해당 Phase에서 결정)
- [x] (Phase 0) GitHub 원격 저장소 사용 여부 → 비공개로 사용
- [ ] (Phase 1) ERP 모듈 선정
- [ ] (Phase 2) 다이어그램 도구 / 순수 SQL vs ORM
- [ ] (Phase 2) auth-service(IAM)를 별도 서버로 분리할지
- [ ] (Phase 4) API 테스트 도구
- [ ] (Phase 4) 입력 검증 방식: 정규식 직접 작성 → 라이브러리(zod 등) 교체 시점
- [ ] (Phase 5) 회원가입 방식 (공개 가입 vs 관리자 생성)
- [ ] (Phase 6) 여러 서비스 동시 실행 도구
- [ ] (Phase 7) 토큰 저장 위치 / UI 스타일 방법
- [ ] (Phase 9) 테스트 도구
- [ ] (Phase 10) Docker 사용 여부 (클라우드 Linux 서버에서는 사용 가능)
- [ ] (Phase 11) 클라우드 업체 선택 (진행 시점의 무료 정책 확인), 도메인 무료/유료

## 📝 메모 (막혔던 점, 질문 등)
- 
