# React Conventions

## Type 정의

- Type은 `type` 키워드를 사용합니다.

```diff
- interface Foo {
-   name: string;
- }
+ type Foo = {
+   name: string;
+ };
```

- `React.FC`를 사용합니다.

```tsx
type Props = {
  children: string;
};

const Foo: React.FC<Props> = (props) => {
  return <div>{props.children}</div>;
};
```

## Event Handler 규칙

- Event Handler는 `on` 접두사를 사용합니다.

```diff
- const handleClick = () => {};
+ const onClick = () => {};
```

- 헨들러를 JSX 문법안에서 사용하지 않습니다.

```tsx
const Foo = () => {
  const [count, setCount] = useState(0);

  return (
    <button
      onClick={() => {
        setCount((prev) => prev + 1);
      }}
      type="button"
    >
      Click Count: {count}
    </button>
  );
};
```

```tsx
const Foo = () => {
  const [count, setCount] = useState(0);

  const onClick = () => {
    setCount((prev) => prev + 1);
  };

  return (
    <button onClick={onClick} type="button">
      Click Count: {count}
    </button>
  );
};
```
