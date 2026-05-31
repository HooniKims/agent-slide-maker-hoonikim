# agent-slide-maker-hoonikim

HyperFrames 슬라이드, 카드뉴스, 오버뷰 제작을 위한 로컬 스킬 배포 묶음이다.

## 다른 프로젝트에 적용

이 폴더의 아래 항목을 대상 프로젝트 루트에 복사한다.

```text
.codex/
.claude/
.cursor/
skills
skills-lock.json
hyperframes.json
design_asset/
design_examples/
AGENTS.md
```

대상 프로젝트에 이미 `AGENTS.md`가 있으면 내용을 덮어쓰기보다 이 폴더의 라우팅 규칙과 디자인 세트 규칙을 병합한다.

## 디자인 세트 사용 방식

- 활성 디자인은 프로젝트 루트의 `design_asset/`에 둔다.
- 예시는 `design_examples/<name>/design_asset/`에 둔다.
- 새 디자인을 만들 때는 예시 폴더를 복사해 `DESIGN.md`, `tokens.json`, `variables.css`, `theme.css`, `typography-options.json`을 함께 갱신한다.
- composition 작성자는 `design_asset/DESIGN.md`를 먼저 읽고, CSS에서는 `variables.css`의 토큰을 우선 사용한다.
- 새 슬라이드 기본 본문 리듬은 현재 결과물과 맞춰 `letter-spacing: -0.02em`, `line-height: 1.5`를 쓴다.

## 포함된 샘플

현재 샘플 디자인 세트:

```text
design_asset/
design_examples/oryzo-ai/design_asset/
```

두 위치의 샘플은 같은 세트다. `design_asset/`는 바로 쓰는 활성 샘플이고, `design_examples/oryzo-ai/design_asset/`는 새 프로젝트에서 복사해 쓰는 예시다.
