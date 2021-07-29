`useTransition`允许延时由`state`改变而带来的视图渲染。避免不必要的渲染。它还允许组件将速度较慢的数据获取更新推迟到随后渲染，以便能够立即渲染更重要的更新。

```react
const TIMEOUT_MS = { timeoutMs: 2000 }
const [startTransition, isPending] = useTransition(TIMEOUT_MS)
```

- `useTransition` 接受一个对象， `timeoutMs`代码需要延时的时间。
- 返回一个数组。**第一个参数：** 是一个接受回调的函数。我们用它来告诉 `React` 需要推迟的 `state` 。**第二个参数：** 一个布尔值。表示是否正在等待，过度状态的完成(延时`state`的更新)。

```react
const SUSPENSE_CONFIG = { timeoutMs: 2000 };

function App() {
  const [resource, setResource] = useState(initialResource);
  const [startTransition, isPending] = useTransition(SUSPENSE_CONFIG);
  return (
    <>
      <button
        disabled={isPending}
        onClick={() => {
          startTransition(() => {
            const nextUserId = getNextId(resource.userId);
            setResource(fetchProfileData(nextUserId));
          });
        }}
      >
        Next
      </button>
      {isPending ? " 加载中..." : null}
      <Suspense fallback={<Spinner />}>
        <ProfilePage resource={resource} />
      </Suspense>
    </>
  );
}
```

在这段代码中，我们使用 `startTransition` 包装了我们的数据获取。这使我们可以立即开始获取用户资料的数据，同时推迟下一个用户资料页面以及其关联的 `Spinner` 的渲染 2 秒钟（ `timeoutMs` 中显示的时间）。

这个`api`目前处于实验阶段，没有被完全开放出来。