---
title: Pinia
date: 2023-01-01 00:00:00
tags: Pinia
layout: aboutPinia
---
# 1.pinia介绍

一个全新的用于Vue的状态管理库，下一个版本的Vuex，也就是Vuex5.0。

之前的vuex主要用于vue2,选项式API；如果想要在vue3中使用vuex，需要使用它的版本4（只是一个过渡的选择，还有缺陷）。故Vue3伴随着组合式API诞生后。设计了全新的Vuex：pinia(也就是vuex5)

* pinia的模块更像一个hooks，不需要嵌套，模块之间可以互相引用，让代码组织更灵活

* 符合Vue3 的 Composition api的风格，可以直接结合vue3的API定义状态，没有嵌套模块

* 没有mutations，只有 state、getters、actions

* vue2和vue3都可以支持

* 支持TypeScript

* 支持Vue DevTools，devtools同样可以追踪到状态的修改

等等.......

pinia从使用角度和vuex几乎是一样的，比vuex等简单了。

vuex有四个核心概念：state、getters、mutations、actions.

pinia有三个：state、getters、actions(同步异步都支持)

---------------------------------------------

vuex当前最新版本是4.x

 * vuex4用于vue3

 * vuex3用于vue2 

pinia当前最新版本是2.x

 * 既支持vue2也支持vue3

 * 可以认为就是vuex5,因为它的作者是官方的开发人员。。。


# 2.pinia的使用

## 一、初始化配置

### 1. 创建项目

npm init vite@latest

(详见Vite 官方中文文档)

### 2. 安装 Pinia

npm install pinia

## 二、基本使用

### 1. 创建 Pinia 实例并挂载

**src/main.js**
```typeScript
import { createApp } from 'vue';
import './style.css';
import App from './App.vue';
import { createPinia } from 'pinia';

// 创建 Pinia 实例
const pinia = createPinia();

// 挂载到Vue根实例
createApp(App).use(pinia).mount('#app');

```
如果使用的是Vue2，还需要安装一个插件，并将创建一个pinia注入到应用的root：
```typescript
import { createPinia, PiniaVuePlugin } from 'pinia'

Vue.use(PiniaVuePlugin)
const pinia = createPinia()

new Vue({
  el: '#app',
  // 其他选项...
  // ...
  // 注意同一个pinia实例可以在多个Vue应用中使用
  pinia,
})
```

### 2.定义 Store

 store 是使用**defineStore()** 定义的，第一个参数是整个应用中store的唯一名称(id)
 
 建议：
 
可以为defineStore()的返回值任意命名，但是最好使用use加上store的名称和Store，例如：useUserStore、useCartStore、useProductStore

```typescript
import { defineStore } from 'pinia'

export const useStore = defineStore('main', {
  // 具体代码...
})
```

### 3. Store中的选项

类似于Vue的选项API，也可以传递一个带有state、actions和getters属性的选项对象

```typescript
export const useCounterStore = defineStore('counter', {
  state: () => ({ count: 0, name: 'Eduardo' }),
  getters: {
    doubleCount: (state) => state.count * 2,
  },
  actions: {
    increment() {
      this.count++
    },
  },
})
```
然而，state就类似于组件的 data ，用来存储全局状态的，getters就类似于组件的 computed，用来封装计算属性，有缓存功能，actions类似于组件的 methods，用来封装业务逻辑，修改 state。

### 4.基本使用

如果你要在组件中使用，就需要先将**store**引入进来，并在**setup()**中声明调用

```typescript
import { useMainStore } from '../store';

export default ({
  setup(){
    const mainStore = useMainStore();
    console.log(mainStore.count); // 这样就可以在组件中获取到Store中的count了
  },
})
```
在模板中使用
```typescript
<template>
    <p>{{ mainStore.count }}</p>
    <p>{{ mainStore.foo }}</p>
</template>
```

那么，这样就会产生一个问题，每次都需要mainStore，这样就很麻烦。

如果你对ES6了解的话可能会想到解构出来。但是这样取出来的数据是有问题的，它已经丢失了响应式，也就是一次性的。

就像上面这段代码，解构出来的数据就已经失去了响应式，如果之后对数据的修改Vue是无法监测到数据变化的。

解决办法：这里就需要使用Pinia为我们提供的**storeToRefs()**API这就类似Vue3中的toRefs()

```typescript
import { storeToRefs } from 'pinia'

export default ({
  setup(){
    const mainStore = useMainStore();
		const { count, foo } = storeToRefs(mainStore);

    return {
      count,
      foo,
    }
  },
})
```
### 5.状态更新和Actions

Actions相当于组件中的方法。它们可以使用defineStore()中的actions属性来定义，并且它们非常适合定义业务逻辑

那么接下来怎么修改数据呢？这里有四种方法来修改。

例如：这里我们需要修改state中的count、foo、arr

**store中**
```typescript
import { defineStore } from 'pinia';

export const useMainStore = defineStore('main', {
  state: () => ({
    count: 100,
    foo: 'bar',
    arr: [1, 2, 3],
  }),
  ...
}
```
**组件中**
```typescript
<template>
    <p>{{ count }}</p>
    <p>{{ foo }}</p>
    <p>{{ arr }}</p>
    <hr />
    <p>
        <button @click="handleChangeState">修改数据</button>
    </p>
</template>

<script setup>
	...
  const handleChangeState = () =>{
    ...
  }
</script>
```

方法一：最简单的方式修改

```typescript
mainStore.count++;
mainStore.foo = 'hello';
```

方法二：如果需要修改多个数据，建议使用 $patch批量更新

```typescript
mainStore.$patch({
  count: mainStore.count + 1,
  foo: 'hello',
  // 由于是以对象形式传递的，显然如果要给数组追加元素不是一个很好的选择
  arr: [...mainStore.arr, 4],
});
```

方法三：更好的批量更新的方法：$patch也可以传递一个函数

```typescript
mainStore.$patch((state) => {
  // 这里接收的形参就是state
  state.count++;
  state.foo = 'hello';
  state.arr.push(4);
});
```

方法四：逻辑比较多的时候可以封装到 actions 里面

组件中
```typescript
mainStore.changeState(); // 在修改数据的方法中可以直接调用这个封装在actions里面的函数
```

```typescript
import { defineStore } from 'pinia';

export const useMainStore = defineStore('main', {
  ...
  actions: {
    // 注意：不能使用箭头函数定义，因为使用箭头函数会导致 this 指向错误
    changeState(num) {
      this.count += num;
      this.foo = 'hello';
      this.arr.push(4);

      // this.$patch({}) // 这里如果批量更新和方法二、三一样
      // this.$patch((state) => {});
    },
  },
}
```

### 6.Getters使用

Getters完全等同于Store state的计算值。

可以使用defineStore()中的getters属性来定义它们，并且它们将state作为第一个参数接收，以鼓励使用箭头函数。

如果你使用的是普通函数的话，这个参数是可选的不接收也可以使用this，

```typescript
export const useMainStore = defineStore('main', {
  state: () => ({
    count: 100,
  }),
  getters: {
    // 函数接收一个可选的参数，是 state 对象
    /* count10(state) {
            console.log('count10 被调用了');
            return state.count * 10;
        }, */

    // 🔴 如果是在ts中的话，this的类型是推导不出来的，所以需要手动指定
    /* count10: number() {
            console.log('count10 被调用了');
            return this.count * 10;
        }, */
    count10: (state) => state.count * 10,
  },
},
```

**src/store/index.js**
```typescript
import { defineStore } from 'pinia';

// 1、定义容器
// 参数1：容器名称 ID ，必须唯一，将来 Pinia 会把所有的容器挂载到根容器
// 参数2：选项对象
// 返回值：一个函数，调用得到容器实例
export const useMainStore = defineStore('main', {
    /**
     * 类似于组件的 data，用来存储全局状态的
     * 1、必须是函数：这样是为了在服务端渲染的时候避免交叉请求导致数据的状态污染
     * 2、必须是箭头函数：这是为了更好的 TS 类型推导
     */
    state: () => ({
        count: 100,
        foo: 'bar',
        arr: [1, 2, 3],
    }),
    /**
     * 类似于组件的 computed，用来封装计算属性，有缓存功能
     */
    getters: {
        // 函数接收一个可选的参数，是 state 对象
        /* count10(state) {
            console.log('count10 被调用了');
            return state.count * 10;
        }, */

        //  如果是在ts中的话，this的类型是推导不出来的，所以需要手动指定(加:number)
        /* count10() {
            console.log('count10 被调用了');
            return this.count * 10;
        }, */
        count10: (state) => state.count * 10,
    },

    /**
     * 类似于组件的 methods，用来封装业务逻辑，修改 state
     */
    actions: {
        //注意：不能使用箭头函数定义，因为使用箭头函数会导致 this 指向错误
        changeState(num) {
            this.count += num;
            this.foo = 'hello';
            this.arr.push(4);

            // this.$patch({})
            // this.$patch((state) => {});
        },
    },
});
// 2、使用容器中的 state

// 3、修改 state

// 4、容器中的 action 的使用

```
**src/components/HelloWord.vue**

```typescript
<template>
  <p>{{ mainStore.count }}</p>
  <p>{{ mainStore.foo }}</p>
  <p>{{ mainStore.arr }}</p>
  <p>{{ mainStore.count10 }}</p>
  <p>{{ mainStore.count10 }}</p>
  <p>{{ mainStore.count10 }}</p>

  <hr />

  <p>{{ count }}</p>
  <p>{{ foo }}</p>

  <hr />

  <p>
    <button @click="handleChangeState">修改数据</button>
  </p>
</template>

<script setup>
  import { storeToRefs } from 'pinia';
  import { useMainStore } from '../store';

  const mainStore = useMainStore();

  console.log(mainStore.count);

  // 这是有问题的，因为这样拿到的数据不是响应式的，是一次性的
  // Pinia 其实就是把 state 数据都做了 reactive 处理了
  // const { count, foo } = mainStore;

  // 解决办法就是使用 storeToRefs
  // 把解构出来的数据做 ref 响应式代理
  const { count, foo } = storeToRefs(mainStore);

  const handleChangeState = () => {
    // 方法一：最简单的方式就是这样
    // mainStore.count++;
    // mainStore.foo = 'hello';

    // 方法二：如果需要修改多个数据，建议使用 $patch 批量更新
    /* mainStore.$patch({
        count: mainStore.count + 1,
        foo: 'hello',
        arr: [...mainStore.arr, 4],
    }); */

    // 方法三 更好的批量更新的方法：$patch 也可以传入一个函数
    /* mainStore.$patch((state) => {
        state.count++;
        state.foo = 'hello';
        state.arr.push(4);
    }); */

    // 方法四：逻辑比较多的时候可以封装到 actions 里面
    mainStore.changeState(10);
  };
</script>
```

pinia和vue-detools
[![image.png](https://i.postimg.cc/6TshCPmD/image.png)](https://postimg.cc/Zvc3SwZc)

# 3."实战"

## 一、环境初始化

### 1.创建项目

npm create vite

然后跟着提示一步步走，使用ts
2.安装pinia
二、基本使用
1.创建pinia示例并挂载
2.基本使用
打开App.vue，砍掉没用的，我们直接使用项目中HelloWorld.vue组件
下面是HelloWorld.vue的内容
从以上几种修改store数据的方式，可以看出pinia的使用非常的简便+灵活，也非常的Composition API。推荐使用后两种方式。
三、购物车案例
1.准备工作
需求说明
商品列表
展示商品列表
添加到购物车
购物车
展示购物车商品列表
展示总价格
订单结算
展示结算状态
页面模板
数据接口
2.开始开发
定义Store
以下代码学习点：
as类型断言
如何在actions中写异步操作
下面的代码，有以下学习点：
type类型合并与过滤
跨容器通信的极致优雅操作
重写组件
src\components\ProductList.vue
Vue
复制代码
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
<template>
  <ul>
    <li v-for="item in productsStore.all">
      {{ item.title }} - {{ item.price }}
      <br>
      <button :disabled="!item.inventory" @click="cartStore.addProductToCart(item)">添加到购物车</button>
    </li>
  </ul>
</template>

<script lang="ts" setup>
import { useCartStore } from '../store/cart';
import { useProdunctsStore } from '../store/products'

const productsStore = useProdunctsStore()
const cartStore = useCartStore()

productsStore.loadAllProducts() // 加载所有数据
</script>
src\components\ShoppingCart.vue
Vue
复制代码
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
<template>
  <div class="cart">
    <h2>我的购物车</h2>
    <p>
      <i>请添加一些商品到购物车</i>
    </p>
    <ul>
      <li v-for="item in cartStore.cartProducts">{{ item.title }} - {{ item.price }} × {{ item.num }}</li>
    </ul>
    <p>商品总价： {{ cartStore.totalPrice }}</p>
    <p>
      <button @click="cartStore.checkOut">结算</button>
    </p>
    <p v-show="cartStore.checkoutStatus">结算{{ cartStore.checkoutStatus }}.</p>
  </div>
</template>

<script lang="ts" setup>
import { useCartStore } from '../store/cart'
const cartStore = useCartStore()
</script>
