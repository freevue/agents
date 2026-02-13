# React Architecture

## 1. 아키텍처 계층 구조 (Strict Layering)

- **[Layer 0: Base UI Components]**: 서비스 로직이 전혀 없는 순수 UI 라이브러리 스타일. `A11y`, `memoization`, `forwardRef` 필수.
- **[Layer 1: Logic Components]**: Layer 0를 조합하여 서비스 기능을 완성하는 계층. `Context` 기반 상태 공유 및 비즈니스 로직 주입.

## 2. 파일 구조 및 명명 규칙 (Project Structure)

- 모든 컴포넌트는 반드시 **폴더 기반**으로 생성합니다.
  - 구조: `components/<ComponentName>/index.tsx`
  - 필요시: `components/<ComponentName>/AGENTS.md` (필수 생성)

## 3. 재귀적 문서화 규칙 (AGENTS.md Generation)

모든 컴포넌트 폴더에는 해당 컴포넌트를 설명하는 `AGENTS.md`를 반드시 포함하며, 아래 내용을 작성하십시오.

1. **Information**: 컴포넌트의 역할, 상태(Internal State), Props 명세(Types).
2. **Usage**: 실제 서비스에서 이 컴포넌트를 사용하는 코드 예시.
3. **Dependencies**:
   - 이 컴포넌트가 의존하는 하위 컴포넌트들의 목록.
   - 각 의존성 항목은 해당 컴포넌트의 `AGENTS.md` 경로(파일 링크)를 명시하여 재귀적인 문서 탐색이 가능하게 합니다. (예: `[Button](./Button/AGENTS.md)`)

## 4. 기술적 강제 사항

- **Rendering Isolation**: 하위 UI의 상태 변화가 상위를 흔들지 않도록 설계.
- **Accessibility First**: WAI-ARIA 명세 미준수 시 불합격.
- **Independence**: 하위 컴포넌트는 서비스 데이터 구조를 절대 몰라야 함.

## 5. 답변 프로세스

요청을 받으면 항상 다음 구조로 답변하십시오:

1. **Component Hierarchy**: 전체적인 구성도 설명.
2. **Implementation**: 폴더 구조에 맞춰 `index.tsx` 코드 제시.
3. **Documentation Service**: 해당 컴포넌트의 `AGENTS.md` 내용 전문 제시 (의존성 문서 링크 포함).
