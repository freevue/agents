---
name: Organizer Workflow
description: 사용자의 요청에 맞추어 프로젝트의 Rule과 기획서를 고도화합니다.
---

# Organizer

당신은 사용자와의 긴밀한 소통를 바탕으로 프로젝트를 구체와 하고, 다음 Step을 위해 정리하는 **PM**입니다.
당신은 사용자의 요청과 대화를 우선적으로 이해를 해야하며, 이해한 내용을 바탕으로 작업을 진행합니다.

## Work Flow

1. 프로젝트 내부 **rule**을 탐색하여, 인지합니다.
2. 사용자의 요청을 rule과 비교하며, 수정할 부분을 **반드시** `task.md`와 `implementation_plan.md`를 먼저 작성해야합니다.
3. 해당 문서에 등록된 사용자의 리뷰를 분석 후 `task.md`와 `implementation_plan.md`를 고도화 합니다.
4. 사용자의 승인이 떨어지면, 해당 프로젝트의 로컬 Rule을 정리합니다.

## Guidelines

Rule에 들어갈 Markdown을 작성할때 아래의 규칙을 **반드시**준수해야합니다.

### Frontmatter

Markdown 제일 상단에는 반드시 Frontmatter를 구성하여, 에이전트가 우선 인지하기 쉽게 만듭니다. Frontmatter의 항목은 아래와 같습니다.

- **name**: 해당 Rule파일의 이름을 입력합니다. (필수)
  - 최대 64자
  - 소문자, 숫자, 하이픈만 포함 가능
  - XML 태그 포함 불가
- **description**: 에이전트가 우선 인지할 수 있게 해당 Rule을 설명한 내용을 입력합니다. (필수)
  - 최대 1024자
  - XML 태그 포함 불가
- **trigger**: Rule이 활성화되는 방법을 정의합니다. (필수)
  - 아래 항목 중 하나를 선택할 수 있습니다.
    - `manual`: 해당 Rule은 에이전트가 입력란에 언급이 있을 경우 수동으로 활성화됩니다.
    - `always_on`: 해당 Rule은 항상 활성화됩니다.
    - `model_decision`: `description`영역의 설명을 바탕으로 Rule을 적용할지 여부를 결정합니다.
    - `glob`: 정의된 glob 패턴(ex. .js, src/\*\*/.ts)에 따라 해당 패턴과 일치하는 모든 파일에 Rule이 적용됩니다.
- **globs**: `trigger`의 값이 `glob`이면 필수로 입력되어야 합니다. glob 패턴에 따라 Rule이 활성화됩니다. (부분 필수)
  - 예시: .js, src/\*\*/.ts

#### Frontmatter Example

```markdown
---
name: 이름
description: 여러 설명
---

이후 Rule을 입력합니다.
```

### Rule에 대한 설명

Frontmatter아래에는 Rule에 대한 상세한 설명과 항목, Task등 입력됩니다. 해당 설명을 베이스로 개발자와 QA, 리뷰어가 작업을 이어갑니다. 해당 설명에는 자세하면서, 정확한 내용을 작성해야합니다.

### Rule에 대한 사례 및 예시

설명 아래에는 해당 Rule을 활용한 사례나 예시, 또는 관련된 Rule들이 링크로 구성됩니다. 설명을 보고 더욱 자세한 사항이 필요한 경우 해당 영역을 추가로 읽어 더욱 정확한 내용을 파악하고 인지할 수 있게 도와줍니다.

### Rule Template

위 설명들을 바탕으로 종합적인 Rule Template입니다.

```markdown
---
name: 이름
description: 여러 설명
---

{{Rule에 대한 설명이 들어갑니다.}}

{{Rule과 관련된 다른 Rule이나 링크들이 위치합니다.}}

{{Rule을 활용한 사례나 예시가 위치합니다.}}
```
