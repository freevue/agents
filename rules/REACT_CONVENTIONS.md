# React Conventions

## Type 정의

- Type은 `type` 키워드를 사용합니다.

```diff
- interface Foo {}
+ type Foo = {}
```

- `React.FC`를 사용합니다.
- `Props`는 구조분해를 하지 않습니다.

```diff
type Props = {
  children: string
}

- const Foo = (props: Props) => {
- const Foo: React.FC<Props> = ({ children }) => {
+ const Foo: React.FC<Props> = (props) => {
  return <div>{props.children}</div>
}
```

## Event Handler 규칙

- Event Handler는 `on` 접두사를 사용합니다.

```diff
- const handleClick = () => {}
+ const onClick = () => {}
```

- Handler는 JSX 문법안에서 사용하지 않습니다.

```diff
const Foo = () => {
  const [count, setCount] = useState(0)

+ const onClick = () => {
+   setCount((prev) => prev + 1)
+ }

  return (
    <button
-     onClick={() => {
-       setCount((prev) => prev + 1)
-     }}
+     onClick={onClick}
      type="button"
    >
      Click Count: {count}
    </button>
  )
}
```

## Component 구조

Component를 구성할때 하위 예시를 참고하세요.

### Compound Component Pattern (컴파운드 컴포넌트 패턴)

주로 UI를 담당하는 컴포넌트를 구성할때 사용하세요.

`Form`과 같이 자체적으로 **Event Handling**이 필요한 경우가 아니면 상태 사용을 최소화하고, UI를 구성하는 데이터의 경우 **props drilling**을 활용하세요.

```plaintext
components/
└── List/
    ├── index.tsx
    ├── Item.tsx
    └── AGENTS.md
```

```tsx
// components/List/Item.tsx

type Props = {
  children: React.ReactNode;
};

const Item: React.FC<Props> = (props) => {
  return <li>{props.children}</li>;
};

export default Item;
```

```tsx
// components/List/index.tsx

import Item from "./Item";

type Props = {
  children: React.ReactNode;
};
type List = {
  Item: typeof Item;
} & React.FC<Props>;

const List: List = (props) => {
  return <ul>{props.children}</ul>;
};

List.Item = Item;

export default List;
```

### Standard Component Pattern (표준 컴포넌트 패턴)

로직을 담당하는 컴포넌트를 구성할때 사용하세요.

주요 로직과 메인 상태들을 관리하며, UI를 구성하는 Component들을 **Child Node**로 가집니다. Component들을 종합하여 **Container**역할을 합니다.

```plaintext
components/
├── Play.tsx       # 단일 파일로 구성할 수 있습니다.
├── AGENTS.md
└── Board/         # 폴더를 활용하여 구성할 수 있습니다.
    ├── index.tsx
    └── AGENTS.md
```

```tsx
const Board: React.FC<Props> = (props) => {
  const [list] = useState([1, 2, 3]);

  return (
    <List>
      {list.map((index) => (
        <List.Item key={index}>Item {index}</List.Item>
      ))}
    </List>
  );
};
```
