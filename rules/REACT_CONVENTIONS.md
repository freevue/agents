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
