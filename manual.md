# Site Manual — Hyungyu Lee Portfolio

## 새 프로젝트 빠르게 추가하기

PDF 포트폴리오처럼 썸네일 없이 데이터만 있는 경우에도 바로 추가할 수 있습니다.

### 썸네일 없이 추가 (일단 올리고 나중에 이미지 붙이기)

`index.html` → `const PROJECTS = [...]` 배열 **맨 앞**에 아래 형태로 추가합니다.
`thumbnail: ""`로 두면 카드에 회색 박스가 표시되고, 나중에 이미지 경로를 채우면 됩니다.

```js
{
  id: "N08",                          // 기존과 겹치지 않는 고유 ID
  title: "프로젝트 이름",
  year: "2025",
  period: "Mar – Jun 2025",
  category: "AI",                     // 카드 첫 번째 태그로 표시됨
                                      // 현재 사용 중인 카테고리:
                                      //   Game, Data Visualization, Interactive Art,
                                      //   Generative Design, Generative Art,
                                      //   Installation, Film, Branding, Metaverse,
                                      //   AI, Systems, Database
  context: "수업명 or 팀/기관",
  tools: ["React", "Python"],
  thumbnail: "",                      // 이미지 없으면 빈 문자열 — 나중에 채울 것
  shortDesc: "카드에 표시되는 한 줄 설명",
  description: "모달에 표시되는 상세 설명.",
  links: [
    { label: "GitHub", url: "https://github.com/..." }
  ]
}
```

### 나중에 썸네일 추가하기

1. `WorksData/` 폴더에 이미지 파일 추가 (PNG 권장, 4:3 비율, 최소 800px)
2. 해당 프로젝트 객체의 `thumbnail` 필드를 수정:
   ```js
   thumbnail: "/WorksData/파일명.png",
   ```
3. 이미지를 여러 장 보여주고 싶으면 `images` 배열도 추가:
   ```js
   images: ["/WorksData/추가1.png", "/WorksData/추가2.png"],
   ```

### 배포

```bash
git add index.html WorksData/파일명.png
git commit -m "Add project: 프로젝트 이름"
git push origin main
```

push 후 1~2분 내 hyungyulee.xyz에 반영됩니다.

---

## 구조 개요

사이트는 `index.html` 단일 파일로 구성됩니다.
CSS는 `style/main.css` 하나로 관리되며, JS는 `index.html` 하단 `<script>` 블록 안에 인라인으로 포함되어 있습니다.

```
/
├── index.html          ← 사이트 전체 (CV + Works 갤러리 + 모달)
├── style/
│   └── main.css        ← 전체 스타일
├── WorksData/          ← 프로젝트 썸네일 이미지
├── works/              ← 개별 작품 상세 페이지 (구버전, 참고용)
├── icons/              ← favicon 파일들
├── IMG_3459.jpeg       ← About 섹션 사진
├── info.md             ← 사이트 전체 내용 정리 문서
└── manual.md           ← 이 파일
```

---

## CV 정보 수정 방법

`index.html`을 열고 해당 섹션을 직접 편집합니다.

### About 텍스트 변경
```html
<!-- index.html, #about 섹션 -->
<p class="about-intro">I am<br>Hyungyu<br>Lee.</p>
<p class="about-bio">소개 문구 여기 수정</p>
```

### Education 추가/수정
```html
<!-- index.html, #education 섹션 -->
<div class="timeline-item">
  <div class="timeline-year">2023</div>       <!-- 연도 -->
  <div class="timeline-content">
    <div class="timeline-title">학교/기관명</div>
    <div class="timeline-sub">세부 내용</div>
  </div>
</div>
```

### Experience 추가/수정
```html
<!-- index.html, #experience 섹션 -->
<div class="timeline-item">
  <div class="timeline-year">2026&mdash;</div>   <!-- 연도 범위 (현재진행: &mdash;) -->
  <div class="timeline-content">
    <div class="timeline-title">회사/기관명</div>
    <div class="timeline-role">직무/역할</div>   <!-- 파란색으로 표시됨 -->
    <div class="timeline-sub">업무 설명</div>
  </div>
</div>
```

**연도 표기 팁:**
- 현재진행: `2026&mdash;` (→ "2026—")
- 기간: `2025&ndash;26` (→ "2025–26")
- 단일연도: `2020`

---

## 프로젝트 추가 방법

`index.html` 하단 `<script>` 블록 안의 `PROJECTS` 배열에 객체를 추가합니다.

### 1. 썸네일 이미지 준비
`WorksData/` 폴더에 이미지 파일을 추가합니다.
권장 형식: PNG, 정사각형(1:1) 또는 4:3 비율, 최소 800px

### 2. PROJECTS 배열에 항목 추가
`index.html`의 `const PROJECTS = [...]` 배열 **맨 앞**에 추가합니다 (최신 작품이 위에 표시됨).

```js
{
  id: "W08",                          // 고유 ID (기존과 겹치지 않게)
  title: "프로젝트 제목",
  year: "2025",                       // 연도 (필터 등에서 사용 가능)
  period: "Spring 2025",              // 표시용 기간
  category: "Interactive Art",        // 카테고리 (필터 버튼으로 분류됨)
                                      //   현재 카테고리: Game, Data Visualization,
                                      //   Interactive Art, Generative Design,
                                      //   Generative Art, Installation, Film,
                                      //   Branding, Metaverse
  context: "수업명 or 팀/기관",
  tools: ["Processing", "Python"],    // 배열로 여러 개 입력
  thumbnail: "/WorksData/파일명.png",
  shortDesc: "카드에 표시되는 한 줄 설명",
  description: "모달에 표시되는 상세 설명. 자세히 쓸수록 좋음.",
  images: [                           // (선택) 추가 이미지 — 없으면 이 줄 삭제
    "/WorksData/추가이미지1.png",
    "/WorksData/추가이미지2.png"
  ],
  links: [                            // (선택) 외부 링크 — 없으면 빈 배열 []
    { label: "Demo Video", url: "https://vimeo.com/..." },
    { label: "GitHub", url: "https://github.com/..." },
    { label: "Live Demo", url: "https://..." }
  ]
}
```

### 3. 결과 확인
브라우저에서 `index.html`을 열면 Works 섹션에 새 카드가 나타납니다.
카드 클릭 시 모달이 열리며 상세 정보가 표시됩니다.

---

## 카테고리 추가

`category` 필드에 새로운 이름을 입력하기만 하면 됩니다. 카드 태그로 자동 표시됩니다.
별도 코드 수정 불필요.

---

## 디자인 수정 방법

### 색상 변경
`style/main.css` 상단의 CSS 변수를 수정합니다:

```css
:root {
  --bg: #fafaf7;        /* 배경색 */
  --text: #0f0f0e;      /* 기본 텍스트 */
  --muted: #787870;     /* 흐린 텍스트 (연도, 설명 등) */
  --accent: #3f5bf6;    /* 강조색 (역할명, Cum Laude 등) */
  --border: #e6e6e0;    /* 구분선 */
  --surface: #f2f2ec;   /* 카드 배경 등 */
}
```

### 섹션 순서 변경
`index.html`에서 `<section>` 블록의 순서를 바꾸면 됩니다.
Nav 링크(`href="#education"` 등)도 함께 수정하세요.

---

## 배포

이 사이트는 **GitHub Pages**로 배포됩니다. (`CNAME: hyungyulee.xyz`)

```bash
git add .
git commit -m "설명"
git push origin main
```

push 후 1~2분 내 반영됩니다.

---

## 파일별 역할 요약

| 파일 | 역할 |
|------|------|
| `index.html` | 사이트 전체 (수정 대부분 여기서) |
| `style/main.css` | 스타일 전체 |
| `WorksData/` | 프로젝트 썸네일 이미지 |
| `IMG_3459.jpeg` | About 섹션 본인 사진 |
| `icons/` | favicon (브라우저 탭 아이콘) |
| `works/` | 구버전 개별 작품 페이지 (참고용, 현재 미사용) |
| `info.md` | 사이트 내용 전체 정리 문서 |
| `manual.md` | 이 파일 |
