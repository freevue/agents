---
name: Rule Architecture
description: 프로젝트의 Rule을 구성할때 참고해야하는 아키텍처입니다.
---

# Rule Architecture

프로젝트의 Rule은 기본적으로 `.agent/rules/` 경로에 위치하며, `.agent/rules/GEMINI.md`를 rule의 root파일로 인식합니다.

## Tree 구조

해당 프로젝트를 구성하는 요소들을 **카테고리별**, **중요도**등으로 분류하여 Tree 구조로 구성합니다. 이때 아래의 규칙은 반드시 준수해야합니다.

- rule tree의 경우 탑다운 방식으로만 구성되며 파악합니다.
- 하위의 rule은 상위의 rule을 link로 추가할 수 없습니다.
- 다른 카테고리에 있는 rule의 경우 서로 link를 추가할 수 없습니다.

아래는 rule tree의 예시입니다.

```plantext
.agent/rules/
├── GEMINI.md             # Root Rule
├── PROJECT_NAME/
│   ├── PROJECT_NAME.md
│   ├── TOOLS.md
│   └── POINT/
│       ├── POINT_A.md
│       ├── POINT_B.md
│       └── ...
└── DOMAIN/
    ├── DOMAIN.md
    ├── DOMAIN_A/
    │   ├── DOMAIN_A.md
    │   └── ...
    ├── DOMAIN_B/
    │   ├── DOMAIN_B.md
    │   └── ...
    └── ...
```

## Link 추가

rule에 대한 Link를 추가하여 연관성을 연결할 때에는 아래의 항목이 반드시 추가되어야 합니다.

- rule 파일에 대한 상대경로
- 해당 rule에 대한 짧은 설명

위 항목을 테이블로 구성하여 리스트업합니다. 아래는 Link 추가 예시입니다.

```markdown
| Rule               | Description       |
| ------------------ | ----------------- |
| [Rule1](File Link) | Rule1에 대한 설명 |
| [Rule2](File Link) | Rule2에 대한 설명 |
```
