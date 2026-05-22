---
name: web-starter
description: 새로운 웹사이트·웹페이지 프로젝트를 시작할 때 사용한다. 사용자가 어떤 종류의 결과물을 원하는지 분류하고(단일 HTML / Next.js 정적 / 풀스택 SaaS), 핵심 질문 몇 개로 의도를 빠르게 잡은 뒤 폴더·시작 파일·디자인 토큰·CLAUDE.md를 자동 스캐폴드한다. B/C 유형은 자동으로 gstack 워크플로우(/office-hours → /design-consultation → 스캐폴드 → /design-review/ship)에 연결된다. "웹페이지 만들고 싶어", "사이트 만들어줘", "사이트 시작", "새 웹사이트", "웹 시작", "프로젝트 시작", "랜딩 만들어줘", "/web-start" 같은 표현이 트리거. 단순히 기존 파일 1개를 만들 때(`html로 빼봐` 등 1회용 출력)는 사용하지 않는다.
---

# Web Starter — 인터뷰 + 스캐폴드 + gstack 연결

> 매번 다른 웹사이트를 만들 때 같은 질문 반복하지 않기 위한 워크플로우 스킬.
> 디자인 원칙은 자동으로 `web-design-principles` 스킬을 따라간다.
> **B/C는 gstack 워크플로우와 자동 연결**되어 디자인 시스템(DESIGN.md)·리뷰·배포까지 일관되게 흐른다.

---

## 큰 그림

```
[사용자 의도]
    ↓
Step 0: 의도 분류 (1회용 / 단순 / 풀스택)
    ↓
Step 1: 유형 분류 A/B/C
    ↓
Step 2: 인터뷰 (유형별 2~7문항)
    ↓
Step 2.5: 페이지 인벤토리 자동 생성  ← B/C만 (레퍼런스 IA 또는 유형별 default + 1~2장 여유)
    ↓
Step 3: gstack /office-hours    ← B/C만 (A는 생략)
        컨셉 forcing question으로 시드 검증
    ↓
Step 4: gstack /design-consultation  ← B/C만
        DESIGN.md 생성 (타이포·컬러·spacing·motion)
    ↓
Step 4.5: OpenSpec 박기  ← B/C만 (스캐폴드 직전)
        openspec/project.md + 첫 change `scaffold-foundation` 4 artifact
    ↓
Step 5: 폴더 스캐폴드 + DESIGN.md 토큰 주입
    ↓
Step 6: Mock data 시드 작성  ← B/C만 (A는 생략)
    ↓
Step 7: web-design-principles 출력 검증
    ↓
Step 8: 다음 액션 안내 (gstack 후속 명령 가이드)
```

A(단일 HTML)는 Step 3·4·6 건너뛰고 가벼운 흐름만 탄다.

---

## Step 0 — 의도 빠르게 분류 (트리거 문구만 보고)

| 문구 패턴 | 분류 | 행동 |
|---|---|---|
| "html로 빼봐", "한 페이지로 정리해줘", 이미 컨텍스트 있음 | **1회용** | 인터뷰 생략, 즉시 단일 HTML 작성 |
| "사이트 만들어줘", "랜딩 만들어줘", 컨텍스트 부족 | **단순 사이트** | Step 1 → 핵심 3개 질문 |
| "서비스 만들어줘", "회원가입 있는 사이트", "결제" | **풀스택 SaaS** | Step 1 → 풀 인터뷰 7개 |

1회용은 인터뷰 없이 진행. 절대 강제로 7개 질문 던지지 않는다.

---

## Step 1 — 유형 분류 (단순/풀스택일 때)

사용자에게 3선택지로 묻기:

```
어떤 형태로 가실래요?
A) 단일 HTML 한 장 — 30분, 정리·소개·스펙 시트
B) Next.js + shadcn/ui 정적 — 며칠, 랜딩·포트폴리오·여러 페이지
C) Next.js + Supabase 풀스택 — 본격, 회원가입·결제·관리자 등
```

---

## Step 2 — 핵심 질문 (선택된 유형별)

> **공통 필수 질문 1 — 참고 레퍼런스**:
> "참고하고 싶은 사이트 링크 있어요? (없으면 보편 원칙만 적용)"
>
> 이유: 본인이 만드는 사이트가 매번 달라짐 (SaaS / 강의 / 개인 프로필 / 이커머스 / B2B 랜딩 / 병원 등). 고정 레퍼런스 4개(`landing-sites/`)는 LMS·SaaS 편향이라 다른 유형엔 안 맞음. 사용자 레퍼런스 링크가 있으면 즉석 분석해서 그 패턴을 차용. 없으면 보편 원칙만 적용. 레퍼런스 링크는 Step 4 `/design-consultation` 시드로도 사용된다.

> **공통 필수 질문 2 — 톤 (3선택지)**:
> ```
> 톤 어떻게 가실래요?
> A) 흑백 모노톤 ⭐ 추천 (바이브코딩 1원칙 — 빈 캔버스에서 출발, 나중에 색 추가가 쉬움)
> B) 햄로그 노랑/검정 (default 톤)
> C) 다른 톤 (말씀해 주세요)
> ```
>
> 이유: 흑백에서 시작하면 디자인 잡기 훨씬 쉬움 + 작업 중 톤 변경도 자유로움. 사용자 미응답 또는 "추천대로" 선택 시 A(흑백) 적용.

#### A) 단일 HTML
- 프로젝트 이름?
- 사이트 유형? (랜딩 / 프로필 / 강의 / 정리시트 / 기타)
- **참고 레퍼런스 링크 있어요?** (공통 1)
- **톤 3선택지** (공통 2)

#### B) Next.js 정적
- 프로젝트 이름?
- 사이트 유형? (랜딩 / 포트폴리오 / 강의 / 회사 소개 / 기타)
- **참고 레퍼런스 링크 있어요?** (공통 1, 1~2개)
- **톤 3선택지** (공통 2)
- 페이지 인벤토리는 **자동 생성** — Step 2.5 참고. 사용자에게 묻지 않는다.

#### C) 풀스택 SaaS
- 프로젝트 이름?
- 사이트 유형? (B2B SaaS / B2C SaaS / 내부 도구 / 강의 플랫폼 / 병원·클리닉 / 기타)
- **참고 레퍼런스 링크 있어요?** (공통 1, 1~2개)
- **톤 3선택지** (공통 2)
- 누가 보나? (개인용 · 고객 라이브 · 내부 도구)
- 데이터 저장? (Supabase 추천)
- 로그인? (Supabase Auth — 비로그인 영역 어디까지인지)
- 호스팅? (Vercel · 로컬 · 기타)
- 마감/규모?

---

## Step 2.5 — 페이지 인벤토리 자동 생성 (B/C만)

> ⚠️ **사용자에게 페이지 목록을 묻지 않는다. 자동 생성한다.**
>
> 이유: 처음부터 넉넉하게 깔아둬야 디자인 시스템·내비게이션·푸터·SEO 메타가 검증된다. 3페이지로 시작하면 추가할 때마다 레이아웃 다시 손봐야 한다.

### 규칙

1. **레퍼런스 있을 때**: 레퍼런스 사이트의 IA(정보구조)를 자동 추출해 동일 + **여유 1~2장**
   - **1순위: `<레퍼런스>/sitemap.xml` 시도** — URL 깊이 그대로 계층 구조 추출 (대부분의 한국 사이트는 SEO용으로 갖고 있음)
   - **2순위: nav 메뉴 재귀 크롤** — `browse` 바이너리로 헤더 메뉴 펼침 → 1depth·2depth 추출 (sitemap 없거나 부실할 때)
   - 대형 사이트(병원·회사)는 메인 6~7 × 하위 7~8 = 40~60페이지까지 나올 수 있음. 거르지 말고 그대로 인벤토리에 박음
2. **레퍼런스 없을 때**: 사이트 규모를 **1번만** 묻고 규모별 + 유형별 default 사용
   ```
   사이트 규모는?
   A) 소형 (8~12페이지)  — 의원·클리닉, 개인 사무소, B2B SaaS 랜딩
   B) 중형 (15~25페이지) — 중형 회사, 강의 플랫폼, 부티크 호텔
   C) 대형 (40~60페이지) — 종합병원·대학병원, 대기업, 이커머스
   ```
3. 출력 시 "이대로 진행합니다. 빼고 싶은 페이지 있으면 말씀"으로 안내. 동의 기다리지 않고 스캐폴드 진행.
4. 각 페이지마다 mock data 필요량 자동 계산 (규모 비례):
   - **목록 페이지**: 소형 12 / 중형 30 / 대형 60~100 row
   - **상세 페이지**: 1 row 풀 디테일 (Step 6 디테일 규약 적용)
   - **랜딩/소개 페이지**: 카피 + 이미지 placeholder
5. **계층 구조 보존** — 인벤토리는 평면 리스트 X, 부모-자식 구조 그대로 출력. App Router 폴더도 그 구조로 생성 (`app/about/history/page.tsx`)

### 사이트 유형별 × 규모별 default 인벤토리

#### 병원·클리닉

**소형 (의원·단일 진료과, 8~12페이지)**
- 홈 / 원장 인사말 / 진료과 (목록+상세) / 의료진 (목록+상세) / 시설 안내 / 오시는 길 / 공지사항 / 문의 / FAQ / 비급여 안내

**중형 (전문병원, 15~25페이지)**
- 병원 소개: 인사말, 비전, 연혁, 시설안내, 오시는길
- 진료과: 진료과 목록 + 진료과별 상세 (4~6개)
- 의료진: 목록 + 의료진별 상세
- 커뮤니티: 공지사항 (목록+상세), FAQ
- 환자안내: 비급여 안내, 진료시간, 문의

**대형 (종합병원·대학병원, 40~60페이지, 메인 6~7 × 하위 7~8)**
- **병원소개** (7): 인사말 / 미션·비전 / 연혁 / 조직도 / 의료진 소개 / 시설 / 오시는 길
- **진료과·센터** (8~12): 진료과 목록 / 각 진료과별 (의료진·진료시간·주요질환·검사·수술) × 6~10개
- **환자안내** (7): 외래/입원/응급/예약/증명서/비급여/진료비
- **건강정보** (5): 건강칼럼 (목록+상세) / 질병정보 / 수술정보 / 검사정보
- **고객참여** (6): 공지사항 (목록+상세) / 이벤트 / Q&A·문의 / 환자후기 / 자원봉사 / 후원
- **채용·교육** (4): 채용공고 (목록+상세) / 의국 / 인턴·전공의 / 교육과정
- **English/中文** (옵션, 미러 트리)

#### B2B SaaS

**소형 (랜딩, 8~12)**: 홈 / 기능 / 가격 / 도입 사례 (목록+상세) / 블로그 (목록+상세) / 회사 소개 / 문의 / FAQ

**중형 (15~25)**: 위 + 솔루션별 페이지 (3~5) + 통합·연동 / 보안·컴플라이언스 / 채용 / 파트너 / 변경 로그

**대형 (40~60)**: 솔루션 카테고리 × 산업별 페이지 매트릭스 + 리소스 센터(블로그·가이드·웹세미나·이벤트·도구) + 고객사 사례 카테고리

#### 강의 플랫폼

**소형 (8~12)**: 홈 / 강의 (목록+상세) / 강사 (목록+상세) / 후기 / FAQ / 문의 / 약관 / 개인정보처리방침

**중형 (15~25)**: 위 + 카테고리별 강의 / 학습 로드맵 / 멤버십 / 마이페이지(수강중/완료/북마크/결제내역) / 커뮤니티

**대형 (40~60)**: 카테고리 × 난이도 매트릭스 + 라이브/녹화 분리 + 자격증·수료증 / 기업교육 / 강사지원 / 어드민 풀

#### 회사 소개

**소형 (8~12)**: 홈 / 회사 소개 / 비전 / 사업 영역 / 연혁 / 채용 / 뉴스 / 문의

**중형 (15~25)**: 위 + IR / CSR·ESG / 보도자료 (목록+상세) / 채용공고 (목록+상세) / 글로벌 진출

**대형 (40~60)**: 사업영역 × 자회사·계열사 매트릭스 + IR(공시·재무·주가·정관) / ESG 카테고리 / 인재상 + 채용 프로세스 + 인터뷰 / 보도자료·뉴스룸 / 글로벌 사이트 미러

#### 이커머스

**소형 (8~12)**: 홈 / 상품 (목록+상세) / 장바구니 / 주문·결제 / 회원가입·로그인 / 마이페이지 / 공지 / 문의

**중형 (15~25)**: 위 + 카테고리별 상품 (5~8) / 리뷰 / 위시리스트 / 쿠폰 / 이벤트 / FAQ / 약관·정책 풀세트

**대형 (40~60)**: 카테고리 × 서브카테고리 풀 + 브랜드관 / 기획전 / 매거진 / 라이브커머스 / 멤버십 등급 / 적립금·포인트 / 1:1 문의 / 게시판 / 어드민

#### 포트폴리오

**소형 (8~12)**: 홈 / 작업 (목록+상세) / 소개 / 연락 / 블로그(옵션)

**중형 (15~25)**: 위 + 작업 카테고리별 / 클라이언트 / 프로세스 / 가격·견적 / 후기

**대형은 보통 회사 소개 유형으로 흡수**

#### 기타·내부 도구
- 기타: 홈 / 주요 콘텐츠 (목록+상세) / 소개 / 문의 / FAQ + 사이트 유형 보고 추가 판단
- 내부 도구: 대시보드 / 주요 엔티티 (목록+상세 × N) / 설정 / 사용자 관리 / 로그

### 공통 부속 페이지 (모든 유형에 자동 추가)

- 404 / Error
- 약관 / 개인정보처리방침 (placeholder, 실제 문구는 사용자 채움)
- C 유형은 **별도 `admin/` 앱**에 자동 추가 (web/ 앱과 분리):
  - `admin/login` — Supabase Auth 로그인
  - `admin/` — 대시보드 홈
  - `admin/inquiries` — 문의 목록·상세·상태 변경
  - `admin/<주요 엔티티>` — 사이트 유형별로 의료진/공지/상품 등 CRUD
  - `admin/users` — 관리자 계정 관리
  - `admin/settings` — 사이트 설정

### 출력 예시 (병원·레퍼런스 있을 때)

```
페이지 인벤토리 (자동 생성):
  공개: 홈 · 원장인사말 · 진료과 목록 · 진료과 상세 · 의료진 목록 · 의료진 상세
        · 시설 안내 · 오시는 길 · 공지사항 · 문의 · FAQ · 비급여 안내
  부속: 404 · 약관 · 개인정보처리방침
  C 추가: /admin · /admin/login · /admin/inquiries

→ 이대로 진행합니다. 빼고 싶은 페이지 있으면 말씀.
```

---

## Step 3 — gstack `/office-hours` 자동 호출 (B/C만)

스캐폴드 직전에 **컨셉 forcing question**을 한 번 통과시킨다. 사용자가 답한 사이트 유형·레퍼런스·페이지 인벤토리를 시드로 `/office-hours` builder mode 호출.

```
사용자 응답 시드 →  /office-hours
   - "이 사이트의 가장 좁은 wedge는 무엇인가?"
   - "비슷한 사이트 대비 desperate specificity는?"
   - "1순위 사용자 한 명을 그려보면?"
```

**저장 위치**: `Desktop\<프로젝트명>\docs\concept.md`

> A(단일 HTML)는 이 단계 **생략**. 1회용 단일 페이지에 forcing question은 과함.

---

## Step 4 — gstack `/design-consultation` 자동 호출 (B/C만)

`/office-hours` 결과 + 레퍼런스 링크 + 톤 선택을 시드로 `/design-consultation` 실행.

산출물: **`Desktop\<프로젝트명>\DESIGN.md`**
- Aesthetic (어떤 분위기)
- Typography scale (h1~h6, body, caption)
- Color palette (primary/secondary/accent/neutral, light/dark)
- Spacing system (4/8/16/24/32...)
- Layout grid
- Motion principles
- 컴포넌트 변형 가이드 (button/card/input)
- 폰트 + 컬러 미리보기 페이지 자동 생성

이 DESIGN.md가 **Step 5 스캐폴드 시 globals.css 토큰의 진짜 출처**가 된다. 단순 톤 12변수가 아니라 풀 디자인 시스템.

> A는 톤 프리셋 12변수만 사용. DESIGN.md 생성 안 함.

---

## Step 4.5 — OpenSpec 박기 (B/C 필수, A 생략)

> ⚠️ **신규 B/C 프로젝트는 시작 시점부터 OpenSpec 풀 적용**. "post-v1 도입" 권장 무효.
>
> 이유: 본질 박제하며 진행하는 패턴 일관성 + 나중에 큰 변경·리팩토링 시 trace 확보. 스캐폴드 자체가 첫 change.

### 생성물

```
Desktop\<프로젝트명>\openspec\
├── project.md                           # 시스템 본질 anchor (정체성·타겟·도메인·톤·스택·메인 섹션 lock·작업 모드)
└── changes\
    └── scaffold-foundation\             # 첫 change (slug 의도 명확하게 변경 가능)
        ├── proposal.md                  # Why / What Changes / Impact
        ├── design.md                    # Architecture / 데이터 / 라우팅 / 컴포넌트 / 토큰
        ├── tasks.md                     # 체크리스트 (스캐폴드부터 7섹션 구현까지)
        └── specs\<spec-name>\spec.md    # ADDED Requirements + Scenario(WHEN/THEN/AND)
```

### 주의

- `concept.md`(Step 3) / `DESIGN.md`(Step 4)는 `openspec/project.md`에 흡수 또는 `docs/` 보존 — **이중 소스 방지**
- Step 5 스캐폴드는 이 change의 `tasks.md`를 따라 진행
- 첫 change `apply` 마감 후 `archive` → 다음 change 진입 일반 사이클
- 시연·데모 단계 명시 시 Supabase 미연결 + `lib/mock/`만 — 정식 빌드 시점에 별도 change로 진입

---

## Step 5 — 폴더 스캐폴드

기본 위치: `Desktop\<프로젝트명>\`

### A) 단일 HTML
```
Desktop\<프로젝트명>\
├── index.html       (templates/single-html.html 기반, 톤 토큰 적용)
└── README.md        (한 줄 설명)
```

### B) Next.js 정적
```bash
cd Desktop && bun create next-app <프로젝트명>
# tailwind, app router, ts 모두 yes
```
+ `globals.css`에 DESIGN.md 토큰 주입 (Step 4 산출물 기반)
+ shadcn 초기화 (`bunx shadcn@latest init`)
+ `DESIGN.md`, `docs/concept.md` 폴더 루트에 배치
+ `lib/mock/` 디렉토리 생성 (Step 6에서 사용)

### C) 풀스택 SaaS — 공개·관리자 **완전 분리** 2앱 구조

> ⚠️ **C 유형은 default로 공개 사이트(`web/`)와 관리자 사이트(`admin/`)를 별도 앱으로 분리한다.**
>
> 같은 Next.js 앱 안에 `/admin` 라우트만 붙이지 않는다. 사용자가 "분리 안 해도 됨"이라고 명시할 때만 단일 앱으로 합친다.
>
> 이유: (1) 보안 경계 명확 — 공개·관리자 빌드 분리되면 관리자 코드 누출 위험 ↓, (2) 번들 분리 — 관리자 코드가 홈페이지 번들에 안 섞임, (3) 디자인 시스템 별도 — 공개는 마케팅 톤, 관리자는 대시보드 톤 (DESIGN.md 2개), (4) 배포 주기 분리 — 공개 사이트와 관리자 따로 배포 가능, (5) 도메인 분리 가능 — `auto-hospital.com` ↔ `admin.auto-hospital.com`.

**구조**:
```
Desktop\<프로젝트명>\
├── web/                       # 공개 사이트
│   ├── app/                   # 홈, 진료과, 의료진, 문의 등 인벤토리
│   ├── lib/
│   │   ├── supabase/          # 익명 키만 사용 (anon key)
│   │   └── mock/              # 공개용 mock data
│   ├── public/
│   ├── middleware.ts          # 비로그인 영역 — 인증 가드 없음
│   ├── DESIGN.md              # 마케팅 톤 디자인 시스템
│   ├── package.json
│   ├── next.config.ts
│   └── .env.example           # NEXT_PUBLIC_SUPABASE_URL, NEXT_PUBLIC_SUPABASE_ANON_KEY
│
├── admin/                     # 관리자 사이트 (별도 Next.js 앱)
│   ├── app/                   # /login, /, /inquiries, /doctors, /notices ...
│   ├── lib/
│   │   ├── supabase/          # 서비스 롤 키 사용 (server only)
│   │   └── mock/              # 관리자용 mock data
│   ├── middleware.ts          # 모든 라우트 Supabase Auth 가드
│   ├── DESIGN.md              # 대시보드 톤 디자인 시스템 (별도)
│   ├── package.json
│   ├── next.config.ts
│   └── .env.example           # SUPABASE_URL, SUPABASE_ANON_KEY, SUPABASE_SERVICE_ROLE_KEY
│
├── supabase/                  # 공통 DB
│   ├── migrations/
│   │   └── 0001_init.sql
│   └── seed.sql               # Step 6 mock data 통합 seed
│
├── shared/                    # 공통 타입·유틸
│   └── types/                 # Supabase 스키마 타입 (web/admin 양쪽에서 import)
│
├── docs/
│   └── concept.md             # /office-hours 결과
│
├── .claude/
│   └── CLAUDE.md              # 프로젝트 계약 (web/admin 위치, DESIGN.md 2개 위치, mock 위치, gstack 명령)
│
└── README.md                  # 두 앱 동시 기동 가이드 (web: 3000, admin: 3001)
```

**배포 가이드** (`README.md`에 자동 박음):
- `web/` → Vercel 프로젝트 1: `<프로젝트명>.com`
- `admin/` → Vercel 프로젝트 2: `admin.<프로젝트명>.com`
- 같은 Supabase 프로젝트 공유 (RLS로 권한 분리)

**로컬 개발**:
```bash
# 터미널 1
cd web && bun dev          # http://localhost:3000

# 터미널 2
cd admin && bun dev -p 3001  # http://localhost:3001
```

**`shared/types/`는 TypeScript path alias로 양쪽에서 import**:
```ts
// web/tsconfig.json, admin/tsconfig.json 모두에
"paths": {
  "@shared/*": ["../shared/*"]
}
```

**예외**: 사용자가 "분리 안 해도 됨" / "한 앱으로" 명시하면 단일 앱 + `/admin` 라우트 구조 사용 (`(admin)` route group + middleware 가드). 이 경우 DESIGN.md 1개로 진행.

---

## Step 6 — Mock Data 디테일하게 시드 (B/C 필수, A 생략)

> ⚠️ **이 단계가 누락되면 나중에 진짜 데이터로 갈아끼울 때 고생한다. 반드시 디테일하게.**

### 원칙

1. **현실적이어야 함** — `Doctor 1`, `Item A`, `Lorem ipsum` 금지. 진짜 같은 한국어 이름·주소·전화번호·시간·금액·문구.
2. **타입 정의 먼저** — `lib/mock/types.ts`에 모든 엔티티의 타입을 박는다. Supabase 스키마와 1:1 매칭.
3. **단일 위치 집중** — 모든 mock은 `lib/mock/` 한 곳에 모은다. 페이지 컴포넌트에 인라인 데이터 절대 금지.
4. **갈아끼우기 쉽게** — `getDoctors()`, `getInquiries()` 같은 함수로 export. 나중에 함수 본문만 Supabase 쿼리로 교체하면 됨.
5. **양은 충분히** — 3~5개로는 UI 깨짐 안 보임. 페이지네이션·필터 검증 가능한 양 (목록은 12~30개, 카드 그리드는 6~12개).
6. **C는 seed.sql까지 자동 변환** — TS mock → SQL INSERT 문 동시 생성해서 `supabase/seed.sql`에 박아둠.

### 구조 예시

```
lib/mock/
├── types.ts              # 모든 엔티티 타입 (Supabase 스키마와 동기화)
├── index.ts              # getXxx() 함수 export 모음
├── seed-meta.ts          # 회사명·연락처·주소 등 사이트 메타
├── doctors.ts            # 의료진 (이름·진료과·경력·사진·소개)
├── departments.ts        # 진료과
├── reviews.ts            # 환자 후기 (이름 익명화, 날짜, 별점, 본문)
├── inquiries.ts          # 문의 샘플 (관리자 화면용)
├── notices.ts            # 공지사항
└── faqs.ts               # 자주 묻는 질문
```

### types.ts 예시 (병원 사이트 가정)

```ts
export type Doctor = {
  id: string;
  name: string;            // 김도현
  position: string;        // 원장 / 전문의
  department: string;      // 정형외과
  career: string[];        // ["서울대학교 의과대학 졸업", "삼성서울병원 정형외과 전공의"]
  specialty: string[];     // ["관절경 수술", "스포츠 손상"]
  photoUrl: string;        // /mock/doctors/kim-dohyun.jpg
  introduction: string;    // 200~400자 본문
};

export type Inquiry = {
  id: string;
  name: string;
  phone: string;           // 010-1234-5678 형식
  email: string | null;
  category: 'reservation' | 'consultation' | 'insurance' | 'other';
  subject: string;
  body: string;
  status: 'new' | 'in_progress' | 'answered' | 'closed';
  createdAt: string;       // ISO
  answeredAt: string | null;
  answer: string | null;
};
```

### doctors.ts 예시 (양·디테일 기준)

```ts
import { Doctor } from './types';

export const doctors: Doctor[] = [
  {
    id: 'doc-001',
    name: '김도현',
    position: '대표원장',
    department: '정형외과',
    career: [
      '서울대학교 의과대학 졸업',
      '서울대학교병원 정형외과 전공의 수료',
      '대한정형외과학회 정회원',
      '前 강남세브란스병원 정형외과 임상강사',
    ],
    specialty: ['무릎 관절경', '스포츠 손상', '인공관절 치환술'],
    photoUrl: '/mock/doctors/kim-dohyun.jpg',
    introduction:
      '환자의 일상으로의 빠른 복귀를 가장 중요하게 생각합니다. 15년간 5,000여 건의 관절경 수술을 집도하며 ...',
  },
  // ... 최소 6명 이상. 진료과별로 다양하게.
];

export function getDoctors(): Doctor[] {
  return doctors;
}

export function getDoctorById(id: string): Doctor | undefined {
  return doctors.find((d) => d.id === id);
}

export function getDoctorsByDepartment(dept: string): Doctor[] {
  return doctors.filter((d) => d.department === dept);
}
```

### 페이지에서 사용

```tsx
// app/doctors/page.tsx
import { getDoctors } from '@/lib/mock';

export default function DoctorsPage() {
  const doctors = getDoctors();
  return <DoctorList doctors={doctors} />;
}
```

나중에 진짜 데이터로 갈아끼울 때:

```ts
// lib/mock/index.ts → lib/data/index.ts 로 옮기고
export async function getDoctors() {
  const supabase = createServerClient();
  const { data } = await supabase.from('doctors').select('*');
  return data ?? [];
}
```

페이지 코드는 한 줄도 안 바뀐다. **이게 mock 디테일의 목적**.

### 체크리스트 (Step 6 완료 기준)

- [ ] `lib/mock/types.ts` — 모든 엔티티 타입 정의 (10개 이상 필드 가진 엔티티는 sub-type 분리)
- [ ] 각 엔티티 mock 파일 — 최소 6개 이상의 row, 진짜 같은 한국어 데이터
- [ ] `getXxx()` 함수로 export — 페이지에서 직접 배열 import 금지
- [ ] C는 `supabase/migrations/0001_init.sql`에 동일 스키마, `supabase/seed.sql`에 동일 데이터 INSERT
- [ ] 이미지 path는 `/mock/<entity>/<slug>.jpg` 규약. 실제 이미지는 placeholder OK, **파일명은 의미 있는 슬러그**
- [ ] 날짜·금액·전화번호·이메일은 한국 포맷
- [ ] 페이지네이션·필터·정렬·검색 동작이 검증되는 양

---

## Step 7 — 디자인 원칙 자동 적용

`web-design-principles` 스킬이 출력 직전 자동 트리거. 흐름·연속성·AI 슬롭 회피 체크리스트 7개 통과 검증.

---

## Step 8 — 첫 결과 출력 + 다음 액션 안내

### A 출력
```
✅ Desktop\<프로젝트명>\index.html 생성 완료
✅ 톤 토큰 적용 완료

다음:
- 브라우저에서 index.html 직접 열기
- 수정은 "<섹션> 추가/변경해줘"로 요청
```

### B/C 출력
```
✅ Desktop\<프로젝트명>\ 생성 완료
✅ docs\concept.md (office-hours 결과)
✅ DESIGN.md (디자인 시스템)
✅ lib/mock/ — <N>개 엔티티, 총 <M>개 row mock 데이터
✅ globals.css 토큰 주입 완료
[C] ✅ supabase/migrations + seed.sql 동기화 완료
[C] ✅ middleware.ts 인증 가드 골격
[C] ✅ .env.example
[B/C] ✅ openspec/project.md + changes/scaffold-foundation/ (apply 진행 상태)

다음 액션 (gstack 명령):
- bun dev 로 로컬 기동
- 페이지 추가:           /plan-eng-review 로 락인 후 구현
- 디자인 변형 비교:        /design-shotgun
- 라이브 시각 QA:         /design-review
- 기능 동작 QA:          /qa
- 배포:                 /ship → /land-and-deploy
- 기능 추가 시 큰 변경:    opsx:propose (OpenSpec — 옵션)

mock → 진짜 데이터 갈아끼우기:
- lib/mock/index.ts 의 getXxx() 함수 본문만 Supabase 쿼리로 교체
- 페이지 코드는 그대로
```

---

## 톤 프리셋

`~/.claude/skills/web-starter/tokens/`:

| 파일 | 분위기 | 용도 |
|---|---|---|
| `neutral.css` ⭐ | 흑백 모노톤 | **추천 default** — 바이브코딩 1원칙 (빈 캔버스 시작, 색 추가 쉬움) |
| `yellow-black.css` | 햄로그 노랑/검정 | 사용자 시그니처 톤 — 강의·콘텐츠 |
| `naverblog.css` | 따뜻한 베이지+검정 | 블로그·에세이 |

A 유형은 이 프리셋만 사용. B/C는 Step 4 `/design-consultation`이 톤 프리셋을 시드 삼아 풀 DESIGN.md를 생성한다.

다른 톤 요청 시 새 파일 추가하고 사용자 톤 메모리에 기록.

---

## 1회용 단일 HTML 단축 경로

이미 컨텍스트가 있고 ("강의 기획 폴더에 정리해" 같은 흐름) 사용자가 "html로 빼봐"만 던질 때:

1. 인터뷰 생략
2. `web-design-principles`만 자동 적용
3. `templates/single-html.html`을 기반으로 즉시 작성
4. 톤 = **흑백 모노톤(`neutral.css`)** default. 단 사용자가 명시적으로 노랑/검정 또는 다른 톤 지정 시 그것 우선
5. Desktop의 현재 작업 폴더에 저장

오늘 햄로그 강의기획 HTML 2장이 이 경로로 작동한 사례.

---

## OpenSpec 통합 (B/C 시작 시점부터 풀 적용)

> ⚠️ Step 4.5에서 첫 진입. 본 SKILL "post-v1 도입" 권장은 무효 — 신규 B/C는 시작 시점부터 박는다.

폴더 구조:
```
Desktop\<프로젝트명>\openspec\
├── project.md             # 시스템 본질 anchor
├── specs\                 # 현재 스펙 (장기 보존, 첫 archive 후 형성)
└── changes\
    ├── scaffold-foundation\   # 첫 change (Step 4.5에서 생성)
    ├── <next-slug>\           # 이후 진행 중 change
    └── archive\<date>-<slug>\ # 완료된 change
```

워크플로우:
```
[첫 사이클 — Step 4.5에서 자동]
opsx:propose scaffold-foundation
  ↓
opsx:apply  ← Step 5~6 스캐폴드 + mock 시드를 tasks.md 따라 진행
  ↓
opsx:archive

[이후 모든 기능 추가 사이클]
사용자 요청 ("이거 만들까요?")
  ↓
opsx:propose <slug>      ← proposal.md + design.md + tasks.md + spec delta
  ↓
/plan-ceo-review         ← 스코프 도전 (큰 기능일 때)
/plan-eng-review         ← 아키텍처 락인 (또는 /autoplan으로 묶음)
  ↓
opsx:apply               ← tasks 따라 구현
  ↓
/qa → /ship → /land-and-deploy
  ↓
opsx:archive             ← 스펙 박제, project.md 갱신
```

---

## gstack 워크플로우 매핑 (참고)

| 사용자 의도 | 명령 | 단계 |
|---|---|---|
| 컨셉 검증 | `/office-hours` | Step 3 자동 |
| 디자인 시스템 만들기 | `/design-consultation` | Step 4 자동 |
| 디자인 변형 비교 | `/design-shotgun` | 사용 중 수동 |
| 라이브 시각 QA | `/design-review` | 배포 전 수동 |
| 기능 동작 QA | `/qa` 또는 `/qa-only` | 배포 전 수동 |
| 새 기능 락인 | `/plan-eng-review` | 큰 기능 추가 시 |
| 풀 리뷰 파이프라인 | `/autoplan` | 큰 변경 시 |
| PR 만들고 배포 | `/ship` → `/land-and-deploy` | 배포 시 |
| 버그 디버깅 | `/investigate` | 버그 발생 시 |
| 보안 감사 | `/cso` | 출시 전 |
| 변경 이력 박제 | `opsx:propose` → `opsx:archive` | OpenSpec 도입 후 |

---

## 안내 톤

인터뷰 시 너무 격식 차리지 않는다. 본인은 빠른 진행 선호 — feedback 메모리 참조:
> "엑셀 매핑 자동 진행 — txt 파일명 주면 확인 없이 바로 시작"

→ 단일 HTML 1회용은 무조건 인터뷰 생략.
→ 풀스택만 7개 질문, B는 5개로 압축, A는 4개로 압축.
→ Step 3·4(office-hours / design-consultation)는 사용자 확인 없이 자동 실행. 결과만 사용자에게 보고.
→ Step 6(mock data) 작성 중간에 사용자에게 "더 만들까요?" 묻지 말고 체크리스트 기준 충족까지 자동 진행.
