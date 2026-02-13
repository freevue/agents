# Code Conventions

> [!NOTE]
>
> 에이전트는 아래의 **핵심 인라인 가이드**를 기본 동작 원칙으로

## 기본 규칙

- **Typescript**를 기본으로 사용합니다.
- **any** 타입은 사용하지 않습니다.
- **Tree Shaking**을 고려하여 코드를 작성합니다.
  - 프로젝트를 구성할때 `package.json`에 `sideEffects: false`를 설정합니다.

## 네이밍 규칙

- 한글자로 구성된 변수 및 상수, 매개변수, 함수는 사용하면 안됩니다.

```diff
- const c = 1
+ const count = 1

- function onClick(e) {}
+ function onClick(event) {}

- for (const i of list) {}
+ for (const item of list) {}
```

- 변수와 상수, 매개변수, 함수는 `camelCase`를 사용합니다.

```diff
- const one_number = 1
+ const oneNumber = 1

- function add_number() {}
- function AddNumber() {}
+ function addNumber() {}
```

- Class 선언의 경우 `PascalCase`를 사용합니다.

```diff
- class one_number {}
- class oneNumber {}
+ class OneNumber {}
```

- 담기는 값과 관련된 의미있는 이름으로 구성합니다.

```diff
- const item = 1
+ const pageIndex = 1
```

## 함수 구성 원칙

- **Curring**을 최대한 활용합니다.

```typescript
function add(targetValue: number, addValue: number): number;
function add(targetValue: number): (addValue: number) => number;

function add(targetValue: number, addValue?: number) {
  if (addValue === undefined)
    return (currentAddValue: number) => add(targetValue, currentAddValue);

  return targetValue + addValue;
}
```

## export 규칙

- 폴더로 구성할때에는 **Barrel File**패턴을 사용합니다.
- 단일 파일로 구성할때에는 **Named Export**를 사용합니다.

### 권장 Barrel File 패턴

- `package.json`에 `"sideEffects": false`를 설정합니다.
- 파일 구조는 아래의 예시처럼 구성합니다.
  - 폴더의 모든 파일은 `index.ts`로 export 합니다.

```plaintext
src/
├── utils/
│   ├── add.ts
│   └── index.ts
└── index.ts
```

```typescript
// utils/add.ts
function add(targetValue, addValue) {
  console.log(targetValue + addValue);
}

export default add;
```

```typescript
// utils/index.ts
export { default as add } from "./add";
```

```typescript
// index.ts
import { add } from "./utils";

add(1, 2);
```

### 권장 Named Export 패턴

- 파일 구조는 아래의 예시처럼 구성합니다.

```plaintext
src/
├── utils.ts
└── index.ts
```

```typescript
// utils.ts
export function add(targetValue, addValue) {
  console.log(targetValue + addValue);
}

export function subtract(targetValue, subtractValue) {
  console.log(targetValue - subtractValue);
}
```

```typescript
// index.ts
import { add } from "./utils";

add(1, 2);
```
