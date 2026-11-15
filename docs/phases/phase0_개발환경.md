# Phase 0. 개발 환경 준비 — 실습 가이드

> **목표**: 코드를 작성하고, 저장(버전 관리)하고, 데이터를 저장할 도구를 갖춘다.
> **예상 시간**: 1~2시간
> 각 Step을 끝내면 `[ ]`를 `[x]`로 바꿔 주세요. 막히면 화면에 나온 메시지를 그대로 Claude에게 붙여넣으면 됩니다.

## 📋 사전 점검 결과 (2026-11-14)

| 항목 | 상태 |
|---|---|
| Node.js | ✅ v24.13.0 |
| npm | ✅ 11.6.2 |
| Git | ✅ 2.53.0, 이름·이메일 설정됨 |
| VS Code | ✅ 설치됨 |
| PostgreSQL | ❌ 미설치 → **Step 4에서 설치** |

---

## Step 1. VS Code에서 터미널 열고 기본 명령어 익히기

> **터미널**: 마우스 대신 **글자로 명령을 내리는 창**입니다. 개발에서는 프로그램 설치·실행을 대부분 터미널에서 합니다.
> **PowerShell**: Windows에 들어 있는 터미널 프로그램(셸)의 한 종류입니다.

1. VS Code 실행 → `파일 > 폴더 열기` → `C:\git\javascript_claude` 선택
2. 메뉴 `터미널 > 새 터미널` (단축키 `` Ctrl + ` ``) → 아래쪽에 PowerShell 창이 열림
3. 아래 명령어를 **한 줄씩 직접 입력**해 보세요.

| 명령어 | 뜻 | 해보기 |
|---|---|---|
| `pwd` | 지금 **어느 폴더에 있는지** 출력 (Print Working Directory) | `pwd` |
| `ls` | 현재 폴더의 **파일 목록** | `ls` |
| `cd 폴더명` | 폴더 **이동** (Change Directory) | `cd docs` |
| `cd ..` | **위 폴더로** 이동 | `cd ..` |
| `mkdir 이름` | 폴더 **만들기** | `mkdir test-folder` |
| `rmdir 이름` | 빈 폴더 **지우기** | `rmdir test-folder` |
| `cls` | 화면 **지우기** | `cls` |

> 💡 **꿀팁**: 폴더/파일 이름을 몇 글자만 치고 `Tab` 키를 누르면 자동 완성됩니다. `↑` 키는 이전 명령을 다시 불러옵니다.

- [ ] Step 1 완료: `pwd` 결과가 `C:\git\javascript_claude`로 나온다

---

## Step 2. VS Code 확장 설치

> **확장(Extension)**: VS Code에 기능을 추가하는 **플러그인**입니다.

왼쪽 사이드바의 블록 모양 아이콘(`Ctrl + Shift + X`)에서 검색해 설치하세요.

| 확장 | 하는 일 |
|---|---|
| **ESLint** | 코드의 **실수·나쁜 습관을 빨간 줄로 알려주는** 검사 도구 (린터) |
| **Prettier - Code formatter** | 저장할 때 코드 **들여쓰기·모양을 자동으로 정리** (포매터) |
| (선택) Korean Language Pack | VS Code 메뉴를 한국어로 |

- [ ] Step 2 완료

---

## Step 3. Git 저장소 만들고 첫 커밋하기

> **Git**: 파일 변경 이력을 저장하는 **버전 관리 도구**. 게임의 **세이브 기능**과 비슷합니다.
> **저장소(Repository)**: Git이 이력을 관리하는 폴더. 안에 숨김 폴더 `.git`이 생깁니다.
> **커밋(Commit)**: 지금 상태를 하나의 **세이브 포인트**로 저장하는 것.
> **브랜치(Branch)**: 이력의 **갈래**. 기본 갈래 이름을 `main`으로 씁니다.

### 3-1. 기본 브랜치 이름을 main으로 설정 (한 번만)
```powershell
git config --global init.defaultBranch main
```

### 3-2. 이 폴더를 Git 저장소로 만들기
```powershell
git init
```
→ `Initialized empty Git repository ...` 가 나오면 성공

### 3-3. `.gitignore` 파일 만들기

> **.gitignore**: Git에 **올리지 않을 파일 목록**. 비밀번호가 든 `.env`, 용량이 큰 `node_modules`는 절대 올리지 않습니다. 🛡️

VS Code에서 프로젝트 맨 위에 `.gitignore` 파일을 새로 만들고 아래 내용을 **직접 입력**하세요.

```gitignore
# 패키지 폴더 (npm install로 언제든 다시 받을 수 있음)
node_modules/

# 🛡️ 비밀값 (DB 비밀번호, JWT 비밀키 등)
.env
.env.*
!.env.example

# 빌드 결과물
dist/
build/

# 로그 / 백업
*.log
*.dump
backups/

# OS / 에디터
.DS_Store
Thumbs.db
.vscode/*
!.vscode/extensions.json
```

> `!`로 시작하는 줄은 "이건 예외로 **올린다**"는 뜻입니다. `.env.example`은 비밀값을 뺀 **견본**이라 공유합니다.

### 3-4. 첫 커밋
```powershell
git status
```
→ 빨간색으로 아직 저장 안 된 파일 목록이 보입니다.

```powershell
git add .
git status
```
→ 초록색으로 바뀜 = **커밋할 준비 완료(Staging)**

> **스테이징(Staging)**: 커밋에 담을 파일을 **골라 담는** 단계. 장바구니에 담기 → 결제(커밋) 순서입니다.

```powershell
git commit -m "docs: 튜토리얼 계획 문서 추가"
git log --oneline
```
→ 방금 만든 커밋 한 줄이 보이면 성공!

> 💡 커밋 메시지 앞의 `docs:`, `feat:`, `fix:`는 **어떤 종류의 변경인지** 표시하는 관례입니다 (Conventional Commits).
> `docs` 문서 / `feat` 새 기능 / `fix` 버그 수정 / `chore` 기타 설정

- [ ] Step 3 완료: `git log --oneline`에 커밋이 1개 보인다

---

## Step 4. PostgreSQL 설치

> **PostgreSQL**: 데이터를 **표(테이블)** 형태로 저장하는 무료 데이터베이스 프로그램.
> 설치하면 내 PC에서 **DB 서버 프로그램이 항상 켜져 있는 상태**(Windows 서비스)가 됩니다.
> **pgAdmin**: PostgreSQL을 **마우스로 관리**하는 프로그램. **psql**: 터미널에서 쓰는 PostgreSQL 명령 도구.

### 4-1. 설치 파일 받기
1. 브라우저에서 `https://www.postgresql.org/download/windows/` 접속
2. **Download the installer** 클릭 → EDB 페이지에서 **최신 버전의 Windows x86-64** 다운로드
   - 설치가 실패하면(구버전 Windows 호환 문제) **한 단계 낮은 버전**으로 다시 시도하고, Claude에게 에러를 알려주세요.

### 4-2. 설치 마법사 설정

| 화면 | 설정 |
|---|---|
| Installation Directory | 기본값 그대로 |
| Select Components | ✅ PostgreSQL Server, ✅ pgAdmin 4, ✅ Command Line Tools, ⬜ Stack Builder(체크 해제) |
| Data Directory | 기본값 그대로 |
| **Password** | `postgres` 관리자(슈퍼유저) 계정의 비밀번호 입력 🛡️ |
| Port | `5432` (기본값) |
| Locale | Default locale |

> 🛡️ **비밀번호 주의**
> - 이 비밀번호는 DB의 **최고 관리자** 비밀번호입니다. 꼭 기억해 두세요 (비밀번호 관리자에 저장 권장).
> - **채팅창(Claude 포함)이나 코드, 문서에 적지 마세요.** 나중에 쓸 땐 `.env` 파일에만 넣습니다.
> - 앱에서는 이 관리자 계정을 쓰지 않고, Phase 4에서 **서비스 전용 계정**을 따로 만듭니다(최소 권한 원칙).

### 4-3. 터미널에서 psql을 쓸 수 있게 PATH 등록

> **PATH(환경변수)**: 터미널이 명령어 프로그램을 **찾아보는 폴더 목록**. 여기에 등록해야 어느 폴더에서든 `psql`을 칠 수 있습니다.

1. `Windows 키` → "**시스템 환경 변수 편집**" 검색 → 실행
2. `환경 변수` 버튼 → 위쪽 "사용자 변수"에서 `Path` 선택 → `편집`
3. `새로 만들기` → `C:\Program Files\PostgreSQL\<버전번호>\bin` 입력 (실제 폴더를 탐색기로 확인)
4. 확인 → **VS Code를 완전히 껐다가 다시 열기** (새 PATH 적용)

### 4-4. 설치 확인
```powershell
psql --version
```
→ `psql (PostgreSQL) 1x.x` 처럼 나오면 성공

```powershell
psql -U postgres -c "SELECT version();"
```
→ 비밀번호를 물어보면 4-2에서 정한 비밀번호 입력 (입력해도 화면에 안 보이는 게 정상)
→ PostgreSQL 버전 정보가 표로 나오면 **DB 서버 접속 성공!**

> **SQL**: DB에게 명령하는 언어. `SELECT version();`은 "버전 정보를 보여줘"라는 뜻입니다.
> `-U postgres`는 "postgres라는 사용자(User)로 접속"이라는 뜻입니다.

### 4-5. pgAdmin으로도 접속해보기
1. 시작 메뉴 → **pgAdmin 4** 실행
2. 왼쪽 `Servers` → `PostgreSQL 1x` 클릭 → 비밀번호 입력
3. `Databases > postgres`가 보이면 성공

- [ ] Step 4 완료: `psql`과 pgAdmin 둘 다 접속된다

---

## Step 5. 마무리

- [ ] 🤝 GitHub 원격 저장소 사용 여부 Claude와 상의
- [ ] `PROGRESS.md` 갱신 (Claude가 함께 해줌)
- [ ] 커밋: `git add .` → `git commit -m "docs: Phase 0 완료"`

### ✅ Phase 0 완료 조건
- 터미널에서 `node -v`, `git --version`, `psql --version`이 모두 나온다
- `git log --oneline`에 커밋이 있다
- pgAdmin으로 DB에 접속된다

## 🆘 자주 나오는 문제

| 증상 | 원인 / 해결 |
|---|---|
| `psql : 'psql' 용어가 ... 인식되지 않습니다` | PATH 미등록 또는 VS Code를 재시작 안 함 → 4-3 다시 확인 |
| `password authentication failed` | 비밀번호 틀림. 대소문자·한/영 키 확인 |
| `could not connect to server` | DB 서비스가 꺼짐 → `Windows 키` → "서비스" → `postgresql-x64-1x` 시작 |
| `git commit` 시 에디터가 열림 | `-m "메시지"`를 빠뜨림. 열린 창은 `:q!` 입력 후 Enter로 빠져나오기 |
| 한글 커밋 메시지가 깨져 보임 | 화면 표시 문제일 뿐 저장은 정상. 계속되면 Claude에게 문의 |
