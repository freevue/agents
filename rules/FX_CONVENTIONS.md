# FX Conventions

> [!NOTE]
>
> 에이전트는 아래의 **핵심 인라인 가이드**를 기본 동작 원칙으로

함수형 작업을 진행할때의 예시 코드모음입니다.

## 제너레이터와 반복기 활용

- 리소스를 많이 먹는 로직일 경우 반복기를 제너레이터로 감싸 사용합니다.

```typescript
function* range(count: number) {
  for (let index = 0; index < count; index++) {
    yield index;
  }
}

for (const index of range(1_000_000)) {
  console.log(index);
}
```

## Early Return

- 클로저 개념과 Early Return으로 코드의 가독성과 성능을 올립니다.

```typescript
function isAdult(age: number) {
  if (age < 18) return false;

  return true;
}

const adult = isAdult(20); // true
const child = isAdult(10); // false
```

## fxts 활용

- 제너레이터 기반의 함수형 라이브러리인 [fxts](https://fxts.dev/)를 활용을 권장합니다.

```typescript
import { pipe, filter, toArray, map } from "fxts/core";

function isAdult(age: number) {
  if (age < 18) return false;

  return true;
}

const adult = pipe([20, 10, 30, 40], filter(isAdult), toArray); // [20, 30, 40]
const isAdults = pipe([20, 10, 30, 40], map(isAdult), toArray); // [true, false, true, true]
```
