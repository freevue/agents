# AGENTS.md Architecture

당신은 이 아키텍처 규칙에 따라 `AGENTS.md` 파일을 생성하고 관리하는 전략적 설계자입니다.

## 핵심 원칙 (Core Principles)

- **Source of Truth**: `AGENTS.md`는 항상 관리 대상 파일의 최신 상태를 반영해야 합니다. 관리 대상 파일이 변경되면 즉시 해당 `AGENTS.md`를 업데이트하세요.
- **RAG-Ready Nodes**: 각 `AGENTS.md`는 독립적인 지식 노드(Node) 역할을 합니다. 에이전트가 필요한 정보를 정확히 탐색(Traversal)할 수 있도록 상대 경로를 통한 유기적 링크 구조를 유지하세요.
- **Maintainability**: 가독성과 컨텍스트 효율을 위해 파일당 **최대 500라인(Lines)** 이내로 작성하며, 범위를 초과할 경우 작은 단위로 분할합니다.

## 운영 규칙 (Rules)

- **Entry Point & Indexing**: 프로젝트 루트의 `AGENTS.md`는 전체 시스템의 'Root Node'이자 'Entry Point' 역할을 합니다. 모든 하위 도메인별 `AGENTS.md` 노드에 대한 링크를 포함하여 에이전트의 탐색 출발점이 되도록 관리하세요. (추가된 부분)
- **Immediate Update**: 파일의 수정, 추가, 삭제가 발생하면 관련된 `AGENTS.md`를 즉시 동기화합니다.
- **Flat Link Structure**: 복잡한 트리 대신, 에이전트가 지식 그래프처럼 탐색할 수 있도록 `Dependencies` 섹션에 관련 노드들을 명시합니다.
- **Optional Verification**: 복잡한 로직이나 API 노출이 있는 경우 에이전트의 자체 검증 로직을 포함하되, 단순 상수나 스키마 파일의 경우 설명 위주로 구성하여 선택적으로 운영합니다.
- **Title Convention**: 메인 제목(# Header)은 반드시 **영어 대문자**로 작성합니다.
- **Mandatory Sections**: `Files`, `Exports`, `Dependencies`, `Example` 섹션은 기본 규격으로 반드시 포함합니다.

## 지원 모델 (Models)

### Google Gemini

| Model Id                                             | Recommended Version (Model Name) | Characteristics                                                                                                                                                                      |
| :--------------------------------------------------- | :------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `gemini-3-pro-preview`, `gemini-3-pro-image-preview` | `Gemini 3 Pro`                   | 멀티모달 이해 부분에서 세계 최고 수준의 모델이자 Google의 가장 강력한 에이전트형 및 바이브 코딩 모델로, 최첨단 추론을 기반으로 더 풍부한 시각화와 더 심층적인 상호작용을 제공합니다. |
| `gemini-3-flash-preview`                             | `Gemini 3 Flash`                 | 속도, 확장성, 최첨단 인텔리전스를 위해 설계된 가장 균형 잡힌 모델입니다.                                                                                                             |
| `gemini-2.5-flash`                                   | `Gemini 2.5 Flash`               | 최고의 가격 대비 성능을 갖추었으며 다양한 기능을 제공하는 모델 2.5 Flash는 대규모 처리, 짧은 지연 시간, 사고력이 필요한 대량 작업, 에이전트 사용 사례에 가장 적합합니다.             |
| `gemini-2.5-flash-lite`                              | `Gemini 2.5 Flash-Lite`          | 비용 효율성과 높은 처리량에 최적화된 가장 빠른 Flash 모델입니다.                                                                                                                     |

### Anthropic Claude

| Model Id            | Recommended Version (Model Name) | Characteristics                                |
| :------------------ | :------------------------------- | :--------------------------------------------- |
| `claude-sonnet-4-5` | `Claude Sonnet 4.5`              | 복잡한 에이전트 및 코딩을 위한 스마트 모델     |
| `claude-haiku-4-5`  | `Claude Haiku 4.5`               | 최첨단에 가까운 지능을 갖춘 가장 빠른 모델     |
| `claude-opus-4-5`   | `Claude Opus 4.5`                | 최대 지능과 실용적 성능을 결합한 프리미엄 모델 |

## TEMPLATE

```markdown
---
name: [Basename] AGENTS.md
description: 이 노드가 관리하는 도메인 및 파일에 대한 요약
trigger: model_decision
model: [Model Id]
tags: [tech-stack, domain, role]
---

# [DOMAIN_NAME_IN_UPPERCASE]

## Files

- 해당 노드가 관리하는 파일 링크 ([BaseName](Relative-Path))
- 관리 대상 파일이 없으면 `None`

## Exports

- 외부 노드에서 참조 가능한 함수, 클래스, 타입 및 주의사항
- 복잡한 로직의 경우 설명 끝에 `(Verification Required)` 명시 가능

## Dependencies

- 이 노드가 지식 그래프를 형성하기 위해 참조하는 다른 `AGENTS.md` 링크
- 예: [`Common Utils`](../common/AGENTS.md)

## Example

- 이 도메인을 사용하는 가장 표준적이고 안전한 코드 스니펫

## Custom Sections (Optional)

- 파일의 성격에 따라 다음 섹션들을 자유롭게 추가/제거하여 중복을 방지함
- `State`, `Properties`, `Test`, `Design Tokens`, `Interaction Patterns` 등
```
