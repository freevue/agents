## Global Settings

- use context7.
- Always respond in **한국어(Korean)**.
- **#대답**이 붙은 경우 질문에 대한 답변만 진행할 것.

## Tech Stack

- **Primary Language**: 별도의 요청이 없다면 모든 코드는 **TypeScript**로 작성하는 것을 원칙으로 합니다. (Python 등 타 언어는 사용자가 명시적으로 요청한 경우에만 사용)

### Frameworks

- React, Remix, Next.js

### Build Tools

- Vite, ESBuild, Webpack

## Coding Paradigm

- **Functional Programming**: 코드는 **함수형 프로그래밍(Functional Programming)** 스타일을 강력히 권장합니다.
  - **Modular Functions**: 거대한 함수 대신, 작고 명확한 **단일 목적의 함수(Single Responsibility Principle)** 단위로 로직을 분리하십시오.
  - **Pure Functions**: 부수 효과(Side-effect)를 최소화하고, 입력에 대해 항상 동일한 출력을 반환하는 순수 함수 작성을 지향하십시오.
  - **Immutability**: 데이터의 직접적인 변경(Mutation)을 피하고, 불변성(Immutability)을 유지하는 패턴을 사용하십시오.

### TypeScript Optimize: Barrel & Export Rules

1. 내보내기 방식 (Export Strategy)

   - 'default export'보다 'named export'를 우선적으로 사용합니다.
   - 이유: 정적 분석을 용이하게 하여 트리쉐이킹(Tree Shaking) 효율을 극대화하기 위함입니다.
   - 예시: `export const Foo = ...`

2. 배럴 파일 구성 (index.ts)

   - 배럴 파일에서는 'export \* from ...' 형식을 사용하여 하위 모듈을 그대로 전달합니다.
   - 예시: `export * from './Foo';`

3. 참조 규칙 (Import Rules)

   - [내부 참조] 동일한 폴더 혹은 하위 폴더 내의 모듈을 참조할 때는 절대 'index.ts(배럴)'를 거치지 않고 실제 파일 경로로 직접 참조(Direct Import)합니다. (순환 참조 방지)
   - [외부 참조] 모듈 외부(다른 도메인/폴더)에서 가져올 때만 배럴 파일을 통해 경로를 단순화합니다.

4. 구조적 최적화

   - 모든 파일을 하나의 거대한 배럴에 몰아넣지 않고, 기능/도메인 단위로 계층화된 배럴 구조를 권장합니다.
   - 타입 정의(types.ts)나 상수(constants.ts)는 가급적 배럴에서 제외하거나 직접 참조하여 런타임 코드와의 의존성을 최소화합니다.

5. 코드 예시 패턴
   - 파일 구조 예시:
     - Foo.ts: `export const Foo = () => { ... };`
     - index.ts: `export * from './Foo';`

## Code Conventions

### Language & Framework

- CSS Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/css.mdc
- Deno Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/deno.mdc
- Keras Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/keras.mdc
- NextJS Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/next-js.mdc
- React Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/react.mdc
- NestJS Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/nestjs.mdc
- Remix Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/remix.mdc
- TailwindCSS Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/tailwind.mdc
- Tensorflow Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/tensorflow.mdc
- Typescript Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/typescript.mdc

### Build & Test Tools

- ESBuild Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/esbuild.mdc
- ESLint Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/eslint.mdc
- Jest Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/jest.mdc
- Playwrite Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/playwright.mdc
- Vite Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/vite.mdc
- Webpack Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/webpack.mdc
- docker Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/docker.mdc

### Infra

- cloudflare Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/cloudflare.mdc

### CI/CD

- Github Actions Rules: https://github.com/sanjeed5/awesome-cursor-rules-mdc/blob/main/rules-mdc/github-actions.mdc

## External Rules

- https://github.com/freevue/agents/blob/main/rules/antigravity-task.mdc

## Architecture Rules

<!-- 추후 추가 예정 -->

## Quality Assurance

<!-- 추후 추가 예정 -->

## Project-Specific Rules

<!-- 추후 추가 예정 -->
