## TypeScript 快速上手

# Type声明基本类型

### 声明字符串类型

```typescript
type Name = string
const str:Name= 'bot
```

### 声明 字符串或数字类型

```typescript
type Id = string|number
const id1:Id = '123'
const id2:Id = 123 
```

### 同时满足两种类型类型为never（写错了可能）

```typescript
type wrongType = string & number
```


![Untitled.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650260991067/PhdZQyfYM.png)

### 可选类型

```typescript
type User = {
	name:string
	age?:number
}
const u:User = {
	name:'shenxin'
}
```

### 只读类型

```typescript
type User = {
	readonly name:string
	age?:number
}
const u:User = {
	name:'shenxin'
}
u.name="bot"//会报错，因为name属性是只读的
```

### 精确类型

```typescript
type Dir= '东'|'南'|'西'|'北'
const d:Dir = '东'// ok!
const d:Dir = '难'// error!
```

## Type声明复杂类型

### 两个对象的或操作

```typescript
type A = {
    t:'a'
    specialForA:string
}
type B = {
    t:'b'
    specialForA:number
}
// 类型C 表示类型是A或B
type C = A | B
const c1:C={
    t:'b',
		// 这里会报错，因为 t:'b',表示他是类型B
    specialForA:'hi'
}
```

### 两个不同对象的与操作

下面没法融合的会报错


![Untitled 1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650261009388/yYVDvKiW9.png)


![Untitled 2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650261021464/w344RYiMQ.png)

这样可以正常融合


![Untitled 3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650261033066/ezoXJX_s5.png)

或者有兼容的与也是可以的


![Untitled 4.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650261046076/_42FLJchy.png)

## Interface只能描述对象和函数的类型

### 基本用法


![Untitled 5.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650261061303/-r7VOnh8y.png)

### 继承


![Untitled 6.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650261071544/1xlF0z8mL.png)

### 泛型

继承的类型是不确定的，支持参数T，相当于一个函数


![Untitled 7.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650261083204/thW2zV3Q2.png)
