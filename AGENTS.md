# agent-slide-maker-hoonikim

## 응답 규칙

- 항상 한국어로 답변한다.
- 작업이 끝났을 때는 요청한 내용을 요약 정리하고, 작업 과정을 요약 설명한 뒤, 결과를 정리한다.

## 설치 형태

이 폴더는 다른 HyperFrames 프로젝트에 그대로 복사해서 쓰는 배포 묶음이다.

필수 구성:

- `skills` 파일은 `.codex/skills`를 가리킨다.
- `.codex/skills/`에는 실제 스킬 원본이 들어 있다.
- `.claude/skills`, `.cursor/skills`는 같은 `.codex/skills`를 참조한다.
- `design_asset/`는 현재 프로젝트에서 쓰는 샘플 디자인 세트다.
- `design_examples/`는 새 디자인 세트를 만들 때 참고할 예시 묶음이다.

## HyperFrames 작업 라우팅

| 작업 | 먼저 사용할 스킬 |
|---|---|
| HTML 기반 영상 composition | `hyperframes` |
| CLI, lint, preview, render | `hyperframes-cli` |
| GSAP 애니메이션 | `gsap` |
| 16:9 발표/설명 슬라이드 | `hyperframes-slide` |
| 인스타그램/SNS 카드뉴스 | `hyperframes-card-news` |
| 정적 오버뷰 생성 | `hyperframes-overview` |
| 오버뷰 Edit 기능 | `hyperframes-overview-edit` |

## 리뷰 흐름

1. 슬라이드나 카드뉴스를 만들면 먼저 `topics/<주제>/overview.html`을 만든다.
2. 오버뷰를 HTTP로 서빙해 사용자가 먼저 확인하게 한다.
3. 사용자가 수정 요청을 하면 `index.html`과 `overview.html`을 함께 반영한다.
4. 사용자가 명시적으로 영상 렌더를 요청한 뒤에만 `npx hyperframes render`를 실행한다.

## 오버뷰 Edit 안정성 규칙

모든 오버뷰에는 수정 작업 중 데이터가 사라지지 않도록 아래 기능을 포함한다.

- 상단에 되돌리기/다시 실행 버튼 `#nav-undo`, `#nav-redo`를 둔다.
- 단축키는 `Ctrl+Z`, `Ctrl+Y`, `Ctrl+Shift+Z`를 지원한다.
- 텍스트 수정, 요소 크기 변경, 삭제, 복구는 history stack에 기록한다.
- `contenteditable` 요소에 포커스가 있을 때 Backspace, Delete, Space, 방향키가 전역 이동이나 요소 삭제로 전달되지 않게 막는다.
- Edit 모드에서 입력, 삭제, Done 클릭 때문에 텍스트가 사라지면 안 된다.
- history snapshot을 복원할 때 썸네일을 갱신하고, Edit 모드가 켜져 있으면 텍스트 요소를 계속 편집 가능 상태로 유지한다.

## 디자인 세트 규칙

새 composition을 만들기 전에 디자인 출처를 반드시 확인한다.

1. 프로젝트 루트에 `design_asset/DESIGN.md`가 있으면 먼저 읽는다.
2. `design_asset/tokens.json`, `variables.css`, `theme.css`, `typography-options.json`을 함께 참고한다.
3. 프로젝트에 디자인 세트가 없으면 `design_examples/<예시명>/design_asset/`를 프로젝트 루트의 `design_asset/`로 복사해서 시작한다.
4. composition에서는 가능한 한 `design_asset`의 CSS 변수와 토큰 이름을 유지한다.
5. 폰트, 자간, 줄간격은 임의값보다 `typography-options.json`과 CSS 변수 값을 우선한다.
6. 현재 슬라이드 기본 리듬은 `letter-spacing: -0.02em`, `line-height: 1.5`다. 새 슬라이드의 `html, body` 기본값도 이 값을 따른다.

## Typography 기본값

새 composition, 카드뉴스, 오버뷰는 Paperlogy를 기본 한글 웹폰트로 우선 사용한다.

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/fonts-archive/Paperlogy/subsets/Paperlogy-dynamic-subset.css">
```

```css
html, body {
  font-family: "Paperlogy", "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
}
```

디자인 예시가 별도 폰트를 지정하면 해당 디자인 세트의 폰트 규칙을 우선한다.

## Lint & Render

HTML composition을 생성하거나 수정한 뒤에는 토픽 경로를 지정해 lint를 실행한다.

```bash
npx hyperframes lint topics/<주제-이름>
```

오류는 반드시 수정한다. 렌더는 사용자가 “영상 만들어줘”, “render 해줘”, “mp4 뽑아줘”처럼 명시적으로 요청했을 때만 실행한다.
