##### 6- Suspense

何为`Suspense`, `Suspense` 让组件“等待”某个异步操作，直到该异步操作结束即可渲染。

```react
const ProfilePage = React.lazy(() => import('./ProfilePage')); // 懒加载
<Suspense fallback={<Spinner />}>
  <ProfilePage />
</Suspense>
```

##### 