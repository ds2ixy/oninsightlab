# On Insight Lab 홈페이지

외부 공개용 정적 웹사이트입니다. 서버나 데이터베이스가 필요 없어서, 폴더를 그대로 올리면 바로 동작합니다.

```
oninsightlab/
├── index.html   ← 홈페이지 본체 (이 파일 하나가 사이트 전체)
├── files/       ← 자료실에 올릴 파일 + 파비콘 + 공유 썸네일
│   ├── On_Insight_Lab_브랜드_비전체계.pdf
│   ├── On_Insight_Lab_CI_가이드.pptx
│   ├── favicon.png
│   └── og-image.png
└── README.md
```

---

## 1. 먼저 할 일 — 연락처 넣기

`index.html`을 메모장이나 VS Code로 열면, 아래쪽 `<script>` 안 맨 위에 설정 블록이 있습니다.
따옴표 사이에 실제 정보만 채우고 저장하세요.

```js
var CONTACT = {
  email:   "contact@oninsightlab.com",
  tel:     "010-8677-2968",
  address: "제주특별자치도 제주시 신대로 145, 1층 L-32호",
  hours:   "평일 09:00 – 18:00",      // 현재 푸터에는 표시하지 않음
  formUrl: ""                       // 구글폼 주소 (3번 참고)
};
```

- 이메일을 넣으면 Q&A 하단에 **이메일로 문의하기** 버튼이 생깁니다.
- `formUrl`은 문의 양식입니다. 설정 방법은 아래 3번에 따로 정리했습니다.
- 빈 칸으로 두면 푸터에 "등록 예정"으로 표시됩니다.
- `formUrl`이 비어 있으면 문의하기의 '온라인 문의' 칸은 숨겨지고, 이메일·전화 안내만 보입니다. (2026-11-05 연락처 입력 완료)

## 2. 자료실에 자료 추가하기

① 파일을 `files/` 폴더에 넣습니다.
② `index.html`의 `RESOURCES` 목록에 아래 한 덩어리를 복사해 붙여넣고 내용을 고칩니다.

```js
{
  title:    "2026 지역 혁신 트렌드 리포트",
  category: "연구보고서",
  desc:     "한 줄 설명",
  file:     "files/2026_trend_report.pdf",
  date:     "2026-10-01"
},
```

- `category`는 **연구보고서 / 브랜드·CI / 발간자료 / 사업안내 / 기타** 중 하나여야 필터 버튼에 걸립니다.
- 파일명에 공백 대신 `_`를 쓰면 주소 오류가 없습니다.
- 자료를 내리려면 그 덩어리를 지우면 됩니다.

> 지금 등록된 브랜드 비전 체계 PDF와 CI 가이드는 예시 겸 실제 자료로 넣어두었습니다.
> 외부 공개를 원치 않으시면 `files/`에서 파일을 지우고 `RESOURCES`의 해당 항목도 삭제하세요.

## 3. 문의 양식 연결하기 (구글폼)

정적 사이트에는 서버가 없어서, 방문자가 쓴 글을 받아 저장하려면 외부 양식이 필요합니다. 구글폼이 가장 간단하고 무료입니다.

**① 구글폼 만들기** — <https://forms.google.com> → 빈 양식. 아래 항목을 권장합니다.

| 질문 | 유형 | 필수 |
|---|---|---|
| 문의 유형 | 객관식 (사업 제휴 / 행사·포럼 / 컨설팅 / 교육·연수 / 기타) | ○ |
| 성함 | 단답형 | ○ |
| 기관·소속 | 단답형 | |
| 회신 휴대폰 (010-0000-0000) | 단답형 | ○ |
| 회신 이메일 | 단답형 | ○ |
| 제목 | 단답형 | ○ |
| 문의 내용 | 장문형 | ○ |

**② 알림 켜기** — 폼 상단 **응답** 탭 → 점 세 개(⋮) → "새 응답에 대한 이메일 알림 받기". 문의가 들어오면 메일이 옵니다.
같은 **응답** 탭의 초록색 스프레드시트 아이콘을 누르면 모든 문의가 구글 시트에 자동으로 쌓입니다.

**③ 주소 가져오기** — 폼 오른쪽 위 **보내기** → `< >` (HTML 삽입) 탭 → `src="..."` 안의 주소만 복사합니다.
`https://docs.google.com/forms/d/e/1FAIpQL.../viewform?embedded=true` 형태입니다.

**④ 붙여넣기** — `index.html`의 `CONTACT` 블록에 넣습니다.

```js
formUrl:    "https://docs.google.com/forms/d/e/1FAIpQL.../viewform?embedded=true",
formHeight: 1200
```

저장하고 새로고침하면 문의하기 페이지 안에 양식이 바로 나타납니다. (주소가 비어 있으면 '온라인 문의' 칸은 자동으로 숨겨지고 이메일·전화 안내만 보입니다)

> **구글 워크스페이스 계정으로 폼을 만들 때 주의** — 기본값이 "조직 내 사용자로 제한"이라 외부 방문자가 제출하지 못합니다.
> 폼 **설정 → 응답 → "oninsightlab.com 및 신뢰할 수 있는 조직의 사용자로 제한"을 끄기**, 그리고 **"이메일 주소 수집"은 '수집 안함' 또는 '응답자 입력'**으로 두세요.
양식 아래쪽이 잘려 보이면 `formHeight` 숫자를 1400, 1600처럼 키우세요.

> 접수된 문의는 담당자(구글 계정)만 봅니다. 홈페이지에는 공개되지 않습니다.

## 4. FAQ 수정하기

`index.html`에서 `자주 묻는 질문` 부분의 `<details>` 블록을 찾아 문구를 고치면 됩니다.
질문은 `<summary>`, 답변은 `<div class="ans">` 안에 있습니다.

---

## 5. 배포 — 셋 중 편한 방법으로

### ★ GitHub Pages (현재 방식 — 저장소: github.com/ds2ixy/oninsightlab, 도메인: oninsightlab.com)

GitHub 하나로 호스팅합니다. 파일을 고쳐 Commit 하면 1~2분 뒤 사이트에 자동 반영됩니다. Cloudflare는 쓰지 않습니다.

**① GitHub Pages 켜기** (처음 한 번)
1. 저장소 → **Settings** → 왼쪽 **Pages**
2. Source: **Deploy from a branch** / Branch: **main** / 폴더: **/ (root)** → **Save**
3. **Custom domain**에 `oninsightlab.com` 입력 → **Save** (저장소에 `CNAME` 파일이 자동으로 생김 — 지우지 마세요)

**② 도메인 DNS 설정** — 도메인은 Google Workspace에서 구매 → DNS는 **Squarespace Domains**에서 관리
1. Google 관리 콘솔(admin.google.com) → **계정 → 도메인 → 도메인 관리** → oninsightlab.com 의 **세부정보 보기/DNS 관리** → Squarespace Domains로 이동 (같은 Google 계정으로 로그인)
   - 바로 가려면 domains.squarespace.com 에서 Google 계정으로 로그인
2. 도메인 선택 → **DNS** → **Custom records** → **ADD RECORD** 로 아래 5개 추가

| 종류 | Host | 값 |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | ds2ixy.github.io |

3. **절대 지우면 안 되는 것**: `Google Workspace` 묶음(MX 레코드), SPF(`v=spf1 include:_spf.google.com`) TXT, DKIM(`google._domainkey`) TXT, `google-site-verification` TXT — 지우면 contact@oninsightlab.com 메일이 끊깁니다.
4. `@` 또는 `www`에 Squarespace 기본값(**Squarespace Defaults**) A/CNAME 레코드가 있으면 **그것만** 삭제 (위 레코드와 충돌)
5. 반영까지 최대 24시간 → GitHub Pages 화면에서 초록색 확인 표시가 뜨면 **Enforce HTTPS** 체크

**이후 수정** — GitHub에서 `index.html` 수정 또는 **Add file → Upload files** 로 덮어쓰기 → **Commit changes**.

### (참고) Cloudflare Pages — 끌어다 놓기 방식

올릴 것은 `index.html`과 `files` 폴더 **두 가지뿐**입니다. 이 README는 올리지 마세요(누구나 볼 수 있게 됩니다).
Claude가 만들어 준 `oninsightlab_cloudflare.zip`을 그대로 올려도 됩니다.

**처음 올릴 때**
1. <https://dash.cloudflare.com> 에 oninsightlab 계정으로 로그인
2. 왼쪽 메뉴 **Workers & Pages** → **Create application** → **Get started** → **Drag and drop your files**
3. 프로젝트 이름: `oninsightlab` 입력 → zip 파일(또는 index.html·files가 든 폴더)을 끌어다 놓기
4. **Deploy site** (또는 **Save and Deploy**) → `https://oninsightlab.pages.dev` 주소가 발급됨
   (이름이 이미 쓰이고 있으면 뒤에 임의의 글자가 붙습니다)

**수정본을 다시 올릴 때**
- 같은 프로젝트 → **Create a new deployment** → **Production** 선택 → 새 zip 끌어다 놓기

**(Cloudflare를 쓸 경우) 도메인 연결**
1. 도메인을 Cloudflare에 등록: 대시보드 첫 화면 **Add a domain**(또는 Add site) → `oninsightlab.com` → Free 플랜
   - 가비아·후이즈 등에서 산 도메인이면, 그 업체 관리 화면에서 **네임서버를 Cloudflare가 알려준 2개로 변경** (반영까지 수 분~최대 24시간)
   - Cloudflare에서 직접 산 도메인이면 이 단계는 이미 끝난 상태
2. **Workers & Pages** → `oninsightlab` 프로젝트 → **Custom domains** → **Set up a custom domain** → `oninsightlab.com` 입력 → 활성화
3. 같은 방법으로 `www.oninsightlab.com`도 추가 (www로 들어와도 열리게)
4. HTTPS 인증서는 자동 발급. 상태가 **Active**가 되면 완료

> 주의: 끌어다 놓기로 만든 프로젝트는 나중에 GitHub 자동 배포로 바꿀 수 없습니다(새 프로젝트를 만들어야 함).
> 파일 하나당 25MB, 전체 1,000개까지 올릴 수 있습니다.


### A. Netlify Drop — 가장 빠름 (5분, 무료)

1. <https://app.netlify.com/drop> 접속
2. `oninsightlab` **폴더째로** 브라우저에 끌어다 놓기
3. 바로 `랜덤이름.netlify.app` 주소가 발급되고 전 세계 누구나 접속 가능
4. Site configuration → Domain management 에서 보유 도메인 연결 (HTTPS 자동)

수정할 때는 파일을 고쳐서 다시 끌어다 놓으면 교체됩니다.

### B. Vercel — 깃 연동해서 계속 관리할 때

1. GitHub에 이 폴더를 저장소로 올림
2. <https://vercel.com> 에서 저장소 import → 설정 없이 Deploy
3. 이후 GitHub에 파일을 고쳐 올릴 때마다 사이트가 자동 갱신

### C. 카페24 / 가비아 등 국내 웹호스팅 — 이미 계정이 있을 때

1. FTP 정보(주소, 아이디, 비밀번호)로 FileZilla 접속
2. `public_html` (또는 `www`) 폴더 안에 `index.html`과 `files` 폴더를 업로드
3. 도메인 주소로 접속하면 바로 표시됨

> 어느 방법이든 **`index.html`과 `files` 폴더는 같은 위치에 나란히** 있어야 자료실 파일이 열립니다.

---

## 6. 도메인 연결

도메인이 아직 없다면 가비아·후이즈·Cloudflare 등에서 구입할 수 있습니다 (`.kr` 기준 연 1~2만 원대).
구입 후 호스팅 업체가 안내하는 네임서버나 A/CNAME 레코드를 등록하면 연결됩니다.
Netlify와 Vercel은 HTTPS 인증서를 자동으로 발급합니다.

---

## 7. 방문자 통계 (Google Analytics 4)

`index.html` 맨 위 `<head>` 안에 자리를 만들어 두었습니다. 측정 ID만 넣으면 작동합니다.

1. <https://analytics.google.com> → (구글 워크스페이스 계정으로 로그인) → **관리(톱니바퀴)** → **만들기 → 속성**
2. 속성 이름 `On Insight Lab`, 시간대 **대한민국**, 통화 **KRW** → 비즈니스 정보 입력
3. 데이터 수집: **웹** → URL `oninsightlab.com`, 스트림 이름 `홈페이지` → **스트림 만들기**
4. 화면에 나온 **측정 ID**(`G-`로 시작) 복사
5. `index.html`에서 `var GA_ID = "";` 따옴표 안에 붙여넣기 → Commit
6. 사이트에 접속한 뒤 Analytics **보고서 → 실시간**에 내 접속이 보이면 완료 (일반 보고서는 24~48시간 뒤부터 쌓임)

- 메뉴로 페이지를 바꿀 때마다 '페이지 조회'로 따로 기록됩니다 (예: `On Insight Lab · archive`)
- 방문자 쿠키를 사용하므로, 개인정보처리방침을 만들 때 "Google Analytics로 방문 통계를 수집한다"는 문구를 넣으세요

## 참고

- **2026-11-05 디자인 개편 반영**: 메인 비주얼(원 클릭 이동), 사업 영역, 아이콘 상단 메뉴(누르면 하위 메뉴 줄), 첫 화면은 메인만 보이는 페이지 보기, 퀵메뉴(사업영역·자료실·문의·밝기·홈·위·아래). 내부용 페이지와 같은 디자인이며, 사업 영역 문구는 내부용에서 수정한 내용 기준입니다. 문구를 바꾸려면 index.html 안의 `AREAS`(기본 문구) 또는 `var saved =` 줄을 고치세요.
- **상단 메뉴**: 반투명 유리(글래스) 효과로, 스크롤하면 뒤 내용이 비쳐 보입니다. 구형 브라우저에서는 자동으로 불투명 배경으로 바뀝니다.
- **퀵메뉴**: 화면 오른쪽에 고정된 빠른 메뉴입니다. 화면 폭 1180px 이하(노트북 작은 화면·태블릿)에서는 자동으로 숨겨집니다.
- **하단 내비게이션 바**: 화면 폭 900px 이하에서 나타나는 스마트폰용 메뉴입니다. 홈·회사소개·비전·자료실·문의하기 5개로, 현재 보고 있는 섹션이 파란색으로 표시됩니다.
- **푸터 사이트맵**: 주요 메뉴가 하위 항목까지 한 번 더 정리되어 있습니다. 메뉴를 늘리거나 줄이려면 `index.html` 아래쪽 `<footer>` 안의 `<li>` 항목을 수정하세요.
- **다크 모드**: 방문자 기기 설정을 따라가고, 푸터 오른쪽 `THEME` 버튼으로 직접 전환할 수 있습니다.
- **모바일**: 별도 작업 없이 화면 폭에 맞춰 조정됩니다.
- **검색·SNS 공유**: 제목, 설명, 공유 썸네일이 들어 있습니다. 도메인 `oninsightlab.com` 기준으로 `og:url`, `og:image`(https://oninsightlab.com/files/og-image.png), `canonical` 주소를 설정해 두었습니다(2026-11-05). 도메인이 바뀌면 이 세 줄을 함께 고치세요.
- **브랜드 규정**: 로고 최소 보호 구역 3a, 디지털 최소 크기 심볼 24px / 조합형 40px, 전용 색상 `#008CD6` `#001333` `#0D0D0D` — CI 가이드 기준을 그대로 적용했습니다.
