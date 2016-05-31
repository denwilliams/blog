---
layout: post
title: Typescript Function Types
tags:
  - softwaredevelopment
  - typescript
---

I keep having to look this up again, so for all my future references...

*Inline params:*

```ts
class MyClass {
  myMethod(callback: (x: string) => void) : void {
    callback('hi');
  }
}

function myFunction(callback: (x: string) => void) : void {
  callback('hi');
}
```

*As an interface*

```ts
interface MyCallback {
  (x: string): void;   
}

class MyClass {
  myMethod(callback: MyCallback) : void {
    callback('hi');
  }
}

function myFunction(callback: MyCallback) : void {
  callback('hi');
}
```

*With generics*

```ts
interface Action<T> {
    (arg: T): void;
}

interface Func<T,TResult> {
    (arg: T): TResult;
}
```
