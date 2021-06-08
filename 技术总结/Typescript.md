# Typescript

## infer

infer最早出现在PR中，表示在extends语句中待推断的类型变量

```
type ParamType<T> = T extends (params: infer P) => any ? P : T
```

使用范例

```typescript
function A () {
  return '123'
}

type Te {
	a: ReturnType<typeof A>
}

type B {
	a: '123'
}

type c = keyof typeof B
type b<T> = T extends c ? '123' : '456'

type d = b<c>
type f = b<Te>
```

## 声明全局interface

```
文件名 xx.d.ts
不需要export inport
```

## 面试题

```typescript
题目一：
接受一个函数，返回这个返回值的类型
type ReturnType<T extends (...args: any) => any> = T extends (...args:any) => infer R? R : any;
```



```typescript
题目二：得到一个构造函数的入参类型
接受一个构造函数，返回构造函数的入参类型
type ConstructorParameters<T extends new (...args: any)=> any> = T extends new (...args: infer P) => any ? P : Never
```



```typescript
题目三：得到一个对象范型的子集类型  Partial
type PA<T> = {[key]: value}
type PA<T> = {[K in keyof T]: T[K]}

exp: 
interface A {
  name: string;
  age: number;
  sex: string;
}
type B = PA<A>
```



```typescript
题目四：得到指定一个对象中指定变量的类型   Pick<T, keyof T>
type Pick<T> = {[key]: value}  联想： function pi(obj, k) {return obj[k]}
type Pick<T, K extends keyof T> = {[P in K]: T[K]}

exp:
type B = PI<A, 'name'｜'age'>
```



```typescript
题目五： 将一个对象中指定变量变成可选类型 
// 获取指定变量的类型
type PI<T, K extends keyof T> = {
  	[P in K]?: T[P]
}
// 从对象中删除指定变量的类型定义
type Exclude<T, U> = U extends T ? never: T
// 将上面两部分合并
type Omit<T, K extends keyof T > = PI<T, Exclude<keyof T, K> >

type OptionalType<T, K extends keyof T> = {
  [P in K]?: T[P]
}&Omit<T, K>

exp: 
type RE = OptionalType<A, 'name'> 
RE = {
  name?: string;
  age: number;
  sex: string;
}
```

## 总结

```typescript
<>  =》 （）  TS与JS比较
给第三方模块定义类型 关键字module
declare module 'jquery' {
	// 在这里添加的类型就都是给jquery加的
	forEach(): any
}
补充：函数的缩写
render(): ReactNode
interface A {
	a(): any // a: ()=> {}
}
const a = {
	a(){}
}就是
const a = {
	a: function(){}
}

reduce/map的类型使用
const array = []
array.map<T, I>(item, index)
```

## 源码

