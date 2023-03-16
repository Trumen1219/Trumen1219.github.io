title: Nuxt3
date: 2022-12-01 00:27:45
tags: Nuxt3
layout: aboutNuxt3
---
# Nuxt3 
## 一、Nuxt3简介和开发环境搭建

Nuxt3是Vue3全家桶的一员，让你能轻松实现SSR网页的制作。Nuxt3比Nuxt2新增加了12项最新的特性，包括可以完全使用Vue3的所有语法，并且对TypeScript的完美支持。

### 1.Nuxt3的简介

Nuxt3是基于Vue3发布的SSR框架，也是Vue全家桶系列的一员。如果你了解Nuxt2，应该也了解Nuxt3的使命和用途。但是如果你不了解，你需要先知道两个概念。

* SPA应用：也就是单页应用，这些多是在客户端的应用，不能进行SEO优化（搜索引擎优化）。

* SSR应用：在服务端进行渲染，渲染完成后返回给客户端，每个页面有独立的URL，对SEO友好。

所以如果你开发的应用是企业网站、商品展示 、博客这类型的展示型网站，就需要使用搜索引擎喜欢的SSR应用。

当我们明白这两个概念后，再来看Nuxt3的使命。因为Vue开发的应用默认是单页应用（SPA应用），但如果你想针对于搜索优化，就需要使用Vue的SSR模式开发，而Nuxt3就是Vue的SSR开发的框架。


### 2.Nuxt3 的安装

安装node

安装vue

创建一个nuxt项目：**npx nuxi init nuxt3-test**

注意：npx是npm从5.2版开始增加的命令，所以说你的 npm 最小版本也要是5.2版本。查看npm版本的命令如下。

npm -v

Nuxt3安装成功页面 上面这段提示，也告诉我们了接下来的三个步骤。

**cd nuxt3-test**

**npm install**来安装项目依赖包。

**npm run dev**来运行项目。

### 3.Nuxt3的优势介绍

当我们动手操作完了，我们再简单介绍一下Nuxt3对比Nuxt2的优势或者说作了那些改进。

更轻量：以现代浏览器为基础的情况下，服务器部署和客户端产物最多减小75倍。

更快：用动态服务端代码来优化冷启动。

Hybird：增量动态生成和其他高级模式现在都成为可能。

Suspense: 导航前后可在任何组件中获取数据。

Composition API : 使用Composition API 和 Nuxt3的composables 实现真正的可复用性。

Nuxt CLI ： 权限的零依赖体验，助你轻松搭建项目和集成模块。

Nuxt Devtools ：专属调试工具，更多的信息和快速修复，在浏览器中高效工作。

Nuxt Kit ：全新的基于 TypeScript 和跨版本兼容的模块开发。

Webpack5 ： 更快的构建速度和更小的构建包，并且零配置。

Vite：用Vite作为你的打包器，体验轻量级的快速HMR。

Vue3 ： 完全支持Vue3语法，这一点特别关键。

TypeScript：由原生TypeScript和ESM构成，没有额外配置步骤。

## 二、 Nuxt3的基础目录结构

Nuxt3的目录结构

默认的项目里就如下几个文件和目录

- .nuxt               // 自动生成的目录，用于展示结果
- node_modules        // 项目依赖包存放目录
- .gitignore          // Git的配置目录，比如一些文件不用Git管理就可以在这个文件中配置
- app.vue             // 项目入口文件，你可以在这里配置路由的出口
- nuxt.config.ts      // nuxt项目的配置文件 ，这个里边可以配置Nuxt项目的方方面面
- package-lock.json   // 锁定安装时包的版本，以保证其他人在 npm install时和你保持一致
- package.json        // 包的配置文件和项目的启动调式命令配置
- README.md           // 项目的说明文件
- tsconfig.json       // TypeScript的配置文件

随着我们的开发目录也会越来越多，比如常用的还有下面三个目录。

- pages               // 开发的页面目录
- components          // 组件目录
- assets              // 静态资源目录
- layouts             // 项目布局目录

## 三、编写Hello World程序
```vue
<template>
  <div>
    <NuxtWelcome />
  </div>
</template>
```
其中**<NuxtWelcom />**就是一个框架自带的组件，我们直接删除就可以，不用纠结删除这个组件。

删除后，在 \components 目录下新建一个文件，叫做HelloWorld.vue 然后编写下面的代码。
```vue
<template>
  <div class="">
    <h1>Hello World</h1>
  </div>
</template>
<script setup>
import {} from "vue";
</script>
<style scoped></style>
```

然后再回到app.vue文件中直接写入这个 HelloWorld组件。【注意这里组件的引入方式是通过小写并连接起来引入的】
```vue
<template>
  <div>
    <hello-world />
  </div>
</template>
```

## 四、Nuxt3页面和约定路由的使用

### 1、Nuxt3创建页面

Nuxt3的一个特点就是约定式开发，讲究的是约定大于配置。用Nuxt3就要遵守Nuxt3的规则一样，框架都已经为你做好各种配置了，你只要遵守规则就可以了。 

当你了解什么是“约定式开发”后，再来看如何创建一个Nuxt3的页面。

我们按照框架约定新建一个pages 的文件夹，然后新建一个文件Demo1.vue 。注意，上面这两个步骤，就是约定开发，你必须这么作，否则框架就不认为你是一个页面。

* VSCode自定义代码片段

这里再分享一个小技巧，比如每次新建一个页面，都会有很多相同的代码，这时候就可以使用VSCode的用户代码片段 功能。

这个功能可以在VSCode界面的左下角的齿轮图标中找到。 找到后新建一个Nuxt的片段就可以了。如下：
```javascript
{
  "nuxt":{
    "prefix":"nuxt",
    "body":[
        "<template>",
            "  <div class=\"\"></div>",
        "</template>",
        "",
        "<script setup>",
        "import {} from 'vue'",
        "</script>",
        "",
        "<style scoped></style>",
    ],
    "description":"nuxt3 Components"
  }
}
```
新建好之后，我们再次回到VSCode中的Demo1.vue页面，直接输入 nuxt 回车后，就会生成一段代码了。

[![image.png](https://i.postimg.cc/kgZBJYFL/image.png)](https://postimg.cc/rD18gJH9)

友情提示：工作中巧用这个功能，可以大大加快开发效率。

新的页面建好了，再补充一下页面内容。

<template>
  <div class=""><h1>Demo01</h1></div>
</template>

**约定路由**

当一个页面建立好以后，如何能访问到这个页面 ? 也是一个不能忽视的问题。既然是约定开发，肯定是有一个约定的。

 首先第一步，我们需要在项目根目录下的app.vue文件中，使用 <Nuxtpage> 标签，这就相当于路由的出口了。

```javascript
<template>
  <div>
    <hello-world />
    <NuxtPage></NuxtPage>
  </div>
</template>
```
比如我们现在这个页面，想要访问到，其实只要在地址栏输入下面的地址就可以了。

http://localhost:3000/demo1

但是如果你使用原来的http://localhost:3000就又访问，会显示404，这时候你可以新建一个 在pages文件夹下index.vue 页面。

```javascript
<template>
  <div class=""><h1>Index Page</h1></div>
</template>
<script setup>
import {} from "vue";
</script>
<style scoped></style>
```
这时候在访问http://localhost:3000就可以访问到页面了。

### 2、NuxtLink标签的使用

Nuxt框架不鼓励我们使用<a> 标签进行跳转，而是使用<NuxtLink></NuxtLink>标签进行跳转。比如我们要从 index.vue页面跳转到demo1.vue页面，就可以使用下面的代码进行跳转。
```javascript
<template>
  <div class="">
    <h1>Index Page</h1>
    <NuxtLink to="/demo1">Demo1.vue</NuxtLink>
  </div>
</template>
```

这个页面写完后，可以到浏览器中预览一下效果。基本就可以看到NuxtLink标签的作用了。这节课我们学习了三个知识，我们进行总结一下。

Nuxt3是约定大于配置的开发。

VSCode 自定义用户代码片段的方法

约定路由和<NuxtLink>标签的使用方法

## 五、Nuxt3动态路由的使用

单参数的传递

单参数的传递只要在页面的文件名中用[ ]扩起来就可以了。比如新建一个页面，叫做 demo2-[id].vue。

-| pages/
---| index.vue
---| demo2-[id].vue

也就是说我们使用[ ]的形式就可以设置一个页面的传参。参数接收可以使用 $route.params.id的形式。
```javascript
<template>
  <div class="">获取的id:{{ $route.params.id }}</div>
</template>
<script setup>
import { } from "vue";
</script>
<style scoped></style>
```

我们去首页制作一个链接。
```javascript
<template>
  <div class="">
    <h1>Index Page</h1>
    <NuxtLink to="/demo1">Demo1.vue</NuxtLink> <br />
    <NuxtLink to="/demo2-38">Demo2.vue</NuxtLink>
  </div>
</template>
<script setup>
import {} from "vue";
</script>
<style scoped></style>
```

这时候再到浏览器预览一下，调整后能得到ID，可以了。

在script里获取参数

上面只是在页面中获取了参数，实际作用并不大。工作中获取参数后，都要进行业务逻辑的处理，所以在```<script>```标签里获取参数，才是真实的开发需求。

```javascript
<template>
  <div class="">获取的id:{{ id }}</div>
</template>
<script setup>
import { ref } from "vue";
const route = useRoute();
const id = ref(route.params.id);
</script>
<style scoped></style>
```

上面的代码通过useRoute( ) 获得了 route 然后通过ref让template可用。

多参数的获取

有人说是不是再写一个括号就可以传递多一个参数了，这种是不行的。如果你要传递是两个参数。你需要建立一个文件夹，然后在文件夹上使用[ ]来确定参数。比如我们要传递一个name的参数过来。就需要把目录和文件建立成这样。

-|  pages/
---| index.vue
---| goods-[name]/
-----| demo2-[id].vue
然后修改一些demo2-[id].vue的文件，修改获取的参数。

```javascript
<template>
  <div class="">获取的id:{{ id }}</div>
  <div class="">获取的name:{{ name }}</div>
</template>
<script setup>
import { ref } from "vue";
const route = useRoute();
const id = ref(route.params.id);
const name = ref(route.params.name);
</script>
<style scoped></style>
```

再到index.vue 修改链接，传递两个参数。

<NuxtLink to="/goods-jspang/demo2-38">Demo2.vue</NuxtLink>

完成后再到浏览器中查看结果，可以看到已经接收到了两个参数。 这节课主要学习了Nuxt3中的动态路由，包括：单参数的传递、多参数的传递和在Script标签里获取参数的方法。

## 六、Nuxt3 嵌套路由的使用

掌握了动态路由后，我们还需要对嵌套路由有所了解。嵌套路由就是路由是两级，但是程序员的页面是一个。也就是说有父级页面，也有子集页面。类似我们的页面嵌套。

* 如何建立一个嵌套路由?

 * 嵌套路由的建立非常容易，用一句话解释为：目录和文件名同名，就制作了一个嵌套路由。

 * 制作一个嵌套路由页面一般需要三步：

  * 建立嵌套路由的文件夹（约定大于配置）

  * 创建和文件夹相同名称的文件（父页面）

  * 在新建文件夹下任意创建子页面

|--pages
|----parent/
|------child.vue
|----parent.vue

先在\pages目录下，新建一个文件夹 parent ，然后在pages目录下再建立一个parent.vue的文件。文件建立好之后，编写代码。

```javascript
<template>
  <div class="">Parent Page</div>
  <!-- 子页面的出口-->
  <NuxtChild></NuxtChild>
</template>
<script setup>
import {} from "vue";
</script>
<style scoped></style>
```

这里的<NuxtChild>就是嵌套路由的出口，所以如果是嵌套路由，就必须要加上这个标签。这是Nuxt的一个内置组件。 有了父页面之后，在新建的parent文件夹下，再建立一个 child.vue子页面。然后编写代码。
```javascript
<template>
  <div class="">Child Page</div>
</template>
<script setup>
import {} from "vue";
</script>
<style scoped></style>
```

然后为了看到效果，我们还需要一个路由链接过来。直接到index.uve增加路由链接。

<NuxtLink to="/parent/child">/parent/child</NuxtLink><br />

多个子页面的制作

在\pages\parent\文件夹下面再新建一个文件 two.vue。然后编写代码。
```javascript
<template>
  <div class="">Two Page</div>
</template>
<script setup>
import {} from "vue";
</script>
<style scoped></style>
```

写完后再到index.vue页面，增加导航路由。

<NuxtLink to="/parent/two">/parent/two</NuxtLink><br />

然后去浏览器查看结果。


## 七、 Nuxt3布局模板 让开发高效起来

布局模板的作用就是你先定义好一个布局页面，然后提取一些通用的UI或代码到可重用的模板中，提高代码复用性，从而降低代码的复杂度，让代码重用性提高。

简单说就是把一些通用的UI代码代码提出来，然后放在一个模板里，使用这个模板的每个页面都拥有这些代码UI了。

**创建布局模板和使用模板**

比如现在新建一个文件夹\layouts然后再里边写编写一个 defalut.vue文件，代码如下。
```javascript
<template>
  <div>
    我是布局模板，default.vue
    <slot />
  </div>
</template>
```
上边这段代码就相当于你创建了一个布局模板。有了这个模板后，可以在任何你想要使用的页面中用<NuxtLayout>标签为页面赋予模板中的内容。比如我们想在每个页面中都赋予这个模板中的内容，就可以在 app.vue 页面中使用这个标签。
```javascript
<template>
  <NuxtLayout name="default">
    <div>
      <hello-world />
      <NuxtPage></NuxtPage>
    </div>
  </NuxtLayout>
</template>
```

这样每个页面都会有布局模板中的效果，因为app.vue是每个页面的出口。

**增加多个插槽**

修改default.vue布局模板，增加第二个插槽，一个叫做one，一个叫做two。
```javascript
<template>
  <div>
    我是布局模板，default.vue
    <slot name="one" />
    ---------
    <slot name="two" />
  </div>
</template>
```

这样编写，一个模板中就有了两个插槽，你可以在页面中通过<template #xxx>的形式来指定对应的模板插槽。 在index.vue中使用多个 <template> 配合模板实现多插槽。

```javascript
<template>
  <NuxtLayout name="default">
    <template #one>
      <div class="">
        <h1>Index Page</h1>
        <NuxtLink to="/demo1">Demo1.vue</NuxtLink> <br />
        <NuxtLink to="/goods-jspang/demo2-38">Demo2.vue</NuxtLink><br />
        <NuxtLink to="/parent/child">/parent/child</NuxtLink><br />
        <NuxtLink to="/parent/two">/parent/two</NuxtLink><br />
      </div>
    </template>
    <template #two> 我是two中的内容 </template>
  </NuxtLayout>
</template>
<script setup>
import {} from "vue";
</script>
<style scoped></style>
```

注意上面的页面就精确的对应了模板的插槽。如果页面都非常相似，可以好好的利用这个模板布局。

这个插槽也可以是多个，只要名字对应正确就可以实现。

个人小感想:

布局模板是非常好的一个创意，布局模板再加上组件化，可以大大提高代码的维护性和复用性。所以你想写出漂亮的代码，可以从这两方面多专研。

## 八、 Nuxt3 组件的编写

Nuxt3中创建一个组件

Nuxt3的所有自定义组件，必须写在`components`目录下，写在这个目录下他会自动加载到页面中，而不用我们自己不断的重复引入到每个页面中。

比如现在要创建一个<TheFooter/> 的组件，我们在项目根目录建立一个文件夹`components` ，然后建立一个文件`TheFooter.vue`。

//目录结构
-|components
----|TheFooter.vue

```javascript
<template>
  <h1>The Footer Box</h1>
</template>
```

这段代码只有一个`<h1>` 标签，在页面中显示出了 The Footer Box 。写好组件后，你可以到任何的页面（page）中进行使用。比如在首页使用他们。 打开`/pages/Index.vue`页面，然后在最下面加入这个组件。

```javascript
<template>
  <NuxtLayout name="default">
    <template #one>
      <div class="">
        <h1>Index Page</h1>
        <NuxtLink to="/demo1">Demo1.vue</NuxtLink> <br />
        <NuxtLink to="/goods-jspang/demo2-38">Demo2.vue</NuxtLink><br />
        <NuxtLink to="/parent/child">/parent/child</NuxtLink><br />
        <NuxtLink to="/parent/two">/parent/two</NuxtLink><br />
      </div>
    </template>
    <template #two>
      <div>我是two中的内容</div>
      <TheFooter />
    </template>
  </NuxtLayout>
</template>
<script setup>
import {} from "vue";
</script>
<style scoped></style>
```

这时候你到浏览器中就可以看到我们刚写的`<TheFooter/>` 组件起作用了。

在布局模板中使用组件

底部，其实是每个页面都需要包括的组件，拿我们可以直接把这个组件放到`布局模板`里是非常合适的选择。在布局模板中使用组件和在普通页面中使用组件没有太大的差别，直接使用就可以了。

这里我们就在`\layouts\default.vue`布局模板中使用。

```javascript
<template>
  <div>
    我是布局模板，default.vue
    <slot name="one" />
    ---------<br />
    <slot name="two" />
    <TheFooter />
  </div>
</template>
```

这时候每个使用了`default.vue`这个布局模板的页面就会有`<TheFooter />`这个组件的存在了。

组件名称的约定

我说了很多会了Nuxt3是约定大于配置的开发模式，所以我们要了解Nuxt3框架对于组件名字的约定。比如按照以前的经验，这个`<TheFooter/>` 组件，习惯写成 <the-footer /> 我们测试一下，如果你这样写在页面里也是生效的。

/layouts/default.vue
```javascript
<template>
  <div>
    我是布局模板，default.vue
    <slot name="one" />
    ---------<br />
    <slot name="two" />
    <TheFooter />
    <the-footer />
  </div>
</template>
```

但是个人建议，你尽量使用大写，因为这样可以区分那些是自定义组件，那些是原生的HTML标签。

我说了这是个人建议，但不是必须的。你也可以编写一个`the-header.vue` 的组件，然后用 <the-header/> 的形式使用这个组件也是完全可以的。

例如下面的两端代码。 在`/components`文件夹下面，新建一个页面 `the-header.vuer`

```javascript
<template>
  <h1>The Header Box</h1>
</template>
```

然后回到layouts文件夹下的defalut.vue下使用。

```javascript
<template>
  <div>
    <the-header />
    我是布局模板，default.vue
    <slot name="one" />
    ---------<br />
    <slot name="two" />
    <TheFooter />
    <the-footer />
  </div>
</template>
```

也是完全可以使用的。由此看来Nuxt3对于组件的使用还是非常方便的，你只要符合自己的习惯就好。

小节总结：
主要简单学习了Nuxt3中组件的创建和使用方法。从学习中可以总结道Nuxt3的组件使用非常方便，不用重复的不断引入，可以使用在页面中，也可以使用在布局模板中。而且对于书写的名字也有很宽泛的随意性。

## 九、Nuxt3-多层级组件、懒加载组件的使用

### 1.多层级组件的引用

多层级组件看似好像很复杂，其实多层级组件就是把一个组件放在一个文件夹里。

在实际工作中组件会非常多，所以会把组件分门别类的放置。那这种有层级的组件，我们要如何引用？

比如在` components`文件夹下面，新建一个 `test`文件夹，然后在test文件夹下面再创建一个 `MyButton.vue`文件。

```javascript
<template>
  <div class=""><button>MyButton</button></div>
</template>
<script setup>
import {} from "vue";
</script>
<style scoped></style>
```

写完这个组件后，最关键的一步，就是在页面里如何引用到这个组件。方法很简单，只要在这个页面的前面加上文件夹的名称就可以了。我们的目录结构如下：

--|components
----|test
------|MyButton.vue

那引用组件的方法就是这样的。

**<TestMyButton />**

如果有很多层级，我们也依照这个规律，加入前缀就可以实现多层级组件的引用了。

这种设计的目的是让框架可以应对复杂项目和多组件的需求，让我们的组件更加有条例。

### 2.组件的懒加载

如果在组件名前面加上Lazy前缀，则可以按需懒加载该组件。懒加载组件的目的是在项目打包的时候包更小。简单理解可以理解为只有在组件显示在页面上时才进行加载。

 比如我们现在要做一个文本，这个文本只有在` show`的值为 true的时候才会显示。然后其他时候他不显示。
```javascript
<lazyText v-if="show" />
```
这时候我们就可以使用懒加载组件。如果不总是需要该组件，这将特别有用。

在`components`文件夹下，新建一个 `LazyText.vue`的文件，然后编写代码如下。

```javascript
<template>
  <div class="">Lazy Text Content</div>
</template>
<script setup>
import {} from "vue";
</script>
<style scoped></style>
```

有了组件之后，我们在新建一个页面`demo2.vue`。然后用一个按钮来控制这个组件的显示和隐藏。

```javascript
<template>
  <div class="">
    <lazyText v-if="show" />
    <button @click="handleClick">显示/隐藏</button>
  </div>
</template>
<script setup>
import { ref } from "vue";
const show = ref(false);
const handleClick = () => {
  show.value = show.value ? false : true;
};
</script>
<style scoped></style>
```

然后到浏览器看一下效果，这种就是懒加载组件的使用。

这种组件也可以用来优化页面的打开速度，比如你有一个几百行的长列表。直接加载会给服务器造成很大压力，如果在其他内容已经完成后，过1-2秒再加载这个长列表，就会给用户很好的体验。也会减少服务器的压力。


## 十、Nuxt3 模块化代码 Composable文件夹的试用

在开发中我们经常会有一些通用的业务逻辑代码，需要模块化管理，这时候就可以试用Composable 这个文件夹来编写。

比如我们常用的显示当前时间，这种常用的通用代码，就可以编写成一个单独的代码段，然后在每个页面进行使用。

Composable中创建time.ts的编写

新建一个文件夹composables 然后在文件夹里边，新建一个文件time.ts ，然后编写下面的代码。这段代码你一定编写过，所以就不给大家讲解里边的具体含义了。你可以直接复制这段代码。

```javascript
export  const getTime=()=>{
  const timezone = 8;
  const offset_GMT = new Date().getTimezoneOffset();
  const nowDate = new Date().getTime();
  const today = new Date(nowDate + offset_GMT * 60 * 1000 + timezone * 60 * 60 * 1000);
  const date = today.getFullYear() + "-" + twoDigits(today.getMonth() + 1) + "-" + twoDigits(today.getDate());
  const time = twoDigits(today.getHours()) + ":" + twoDigits(today.getMinutes()) + ":" + twoDigits(today.getSeconds());
  const timeString ='当前时间：' + date + '  ' + time;
  return timeString;
}
function twoDigits(val) {
  if (val < 10) return "0" + val;
  return val;
}
```
写完之后，如何在页面中使用呢？在pages 文件夹下面，新建一个\pages\demo3.vue 的文件，然后你就可以直接在这个页面中使用刚才写的获得时间的方法了。
```javascript
<template>
  <div class="">{{ time }}</div>
</template>
<script setup>
import { ref } from "vue";
const time = ref(getTime());
</script>
<style scoped></style>
```

打开浏览器就可以获得当前时间了。 你可以把任何你在项目中经常使用的代码，封装到这个文件夹里，实现代码的复用。这个文件夹的功能和组件很相似，只是组件是UI部分的代码复用，而这个是业务逻辑代码的复用。

* composables的引入规则

composables 文件夹的引入规则是，只有顶层文件会被引入。也就是说我们如果在这个文件下再新建一个文件夹，是不会被引入到 页面中实现代码复用的。 比如下面的文件格式就没办法引入。

--|composables
----|test
------|test.ts

但是有一种是例外的，就是我们可以写成下面的这种形式。

--|composables
----|test
------|index.ts

我们这里测试一下，新建一个\test 文件夹，然后在它的下面再创建一个index.ts 文件。写入下面的代码。
```javascript
export const test = ()=>{
  console.log('jspang.com')
}
```

然后回到Demo3.vue 页面使用test( ) 方法，结果是可以使用这个方法的。
```javascript
<template>
  <div class="">{{ time }}</div>
</template>
<script setup>
import { ref } from "vue";
const time = ref(getTime());
test();
</script>
<style scoped></style>
```

我们在\test 文件夹下面，再新建一个test.ts 文件，然后编写代码，如下：
```javascript
export const testTwo = ()=>{
  console.log('hello');
}
```
你会发现，这种形式是不能直接引入到页面当中进行使用的，会直接报错`testTwo is not defined`.也就是找不到这个方法。

小节总结
这节主要学习了Nuxt3中业务逻辑代码的复用。你可以把每个页面都使用的代码放在composables 文件夹中，然后按需使用就好。

但是也要有个度，虽没有依据，如果这种方法多起来，会造成页面性能的下降。毕竟每个方法都会引导页面中。

## 十一、Nuxt3中的数据请求

Nuxt3中提供了四种方法：**useAsyncData** 、**useFetch** 、**useLazyFetch** 、**useLazyAsyncData** 。

提供的四个方法，都是获取后台数据的，但是使用场景和使用方法有所不同。

本节练习使用的请求URL：http://121.36.81.61:8000/getTenArticleList （可以获得博客上的10条文章目录）

### 1、**useAsyncData的使用**

使用useAsyncData 异步获取数据，它可以使用在页面中，组件和插件中。我们先通过这个方法来获取一下服务端的数据。 在pages文件夹下，新建一个页面，然后编写下面的代码。
```javascript
<template>
  <div class="">{{list}}</div>
</template>
<script setup>
import {} from "vue";
const res = await useAsyncData("getList", () =>
  $fetch("http://121.36.81.61:8000/getTenArticleList")
);
const list = ref(res)
//const list = ref(res.data._rawValue.data)得到数据
</script>
<style scoped></style>
//$fetch( )方法是nuxt3提供的内置方法，我们直接可以使用。
```

写完后，可以打开浏览器的调试面包，在终端里可以看到返回值是一个对象，对象里有四个属性。

* data: 返回的数据，我们需要的服务器数据就在这个属性里。

* error：是否存在错误，如果存在错误，可以在这个属性中获得，返回的是一个对象。

* pending：这次请求的状态，返回的是布尔值。

* refresh：这个返回的是一个函数，可以用来刷新 handler函数返回的数据。

  * 这个方法的一个特点是，它可以进行很多选项的配置，但是在真实开发中，其实我们用的不多。

  * 最常用的就是lazy 选项，比如我们设置成true 就是需要数据都返回后，才会显示出来 ，简单说就是会阻塞页面。默认是false。

  * 比如要设置lazy为true，就可以这样写。因为我们的数据太少，所以基本看不出来效果。
```js
const res = await useAsyncData(
  "getList",
  () => $fetch("http://121.36.81.61:8000/getTenArticleList"),
  {
    lazy: true,
  }
);
```
这个可配置的选项option 其实还是挺多的，有七项。如果想详细了解的，可以到官方去看一下，地址：

https://v3.nuxtjs.org/api/composables/use-async-data

但这些选项在开发中很少被配置，一般都使用默认值。所以Nuxt3又提供了一个简单的方法useFetch 。

### 1、**useFetch**的使用

useFetch 可以理解为所有的都选择默认配置的useAsyncData 方法。比如还是上面的请求，我们就可以写成下面的形式。

const res = await useFetch("http://121.36.81.61:8000/getTenArticleList");

这样我们依然可以获取数据，当然也是可以传递参数和配置请求方法的。比如我们要设置请求方法是get，传递id是1, 就可以写成下面的形式。

const res = await useFetch("http://121.36.81.61:8000/getTenArticleList", {
  method: "get",
  id: 1,
});

现在我们要把获取到的数据，显示在页面上。修改一下程序，定义变量，然后用ref来赋值就可以了。
```javascript
<template>
  <div class="">{{ list }}</div>
</template>
<script setup>
import { ref } from "vue";
const res = await useFetch("http://121.36.81.61:8000/getTenArticleList");
const list = ref(res.data._rawValue.data);
console.log(res);
</script>
<style scoped></style>
```
这样就可以在页面上看到这些从后端得到的数据了。在实际开发中，我们会把这个数组循环输出，并制作一个精美的列表。

当我们会使用了useAsyncData 和 useFetch 这两个方法后，useLazyAsyncData 和useLazyFetch 也自然会使用了。他们只是把配置选项中的Lazy 设置成了true， 也就是会阻塞页面。 

## 十二、Nuxt3 middleware路由中间件

Nuxt3提供了路由中间件的概念，你可以在整个应用使用它，目的是在导航到某一个页面之前，执行一些代码。最常见的路由守卫就可以用这个实现。

### 1.中间件的基本格式

我们先写一个最简单的中间件，就是在控制台打印来的页面，和要去的页面。目的是通过最简单的实例来了解中间件的基本格式。 

在项目根目录，新建一个middleware的文件夹，然后在文件下边新建一个文件default.global.ts 的文件。

其中的.global代表这个中间件是全局的，也就是在每次跳转都会执行下面的代码。

```js
export default defineNuxtRouteMiddleware((to, from) => {
  console.log("要去那个页面:"+to.path)
  console.log("来自那个页面:"+from.path)
})
```

写完之后，我们可以到浏览器看一下效果。如果一切正常，你可以看到，这时候你在每次跳转时，都会在终端中打出结果。

当然我们可以继续编写代码，看看to 和from里到底都有什么属性。

```js
export default defineNuxtRouteMiddleware((to, from) => {
  console.log("要去那个页面:"+to.path)
  console.log(to)
  console.log("来自那个页面:"+from.path)
  console.log(from)
})
```

可以看到里边的内容是非常多的，特别是to的时候，你可以根据这些来进行编程。

### 2.通过中间件 设置路由守卫

当我们了解路由中间件的基本写法后，在增加一些难度，来模仿一下路由守卫。

比如我们要访问的页面是`http://localhost:3000/demo1`，现在设置路由守卫，不允许访问，而是跳回到首页。那代码就可以写成下面的样子。

```js
export default defineNuxtRouteMiddleware((to, from) => {
  if (to.path === '/demo1') {
     console.log('禁止访问这个页面')
     abortNavigation()  //停止当前导航，可以使用error进行报错
     return  navigateTo('/')
  }
})
```
这时候再到浏览器访问demo1 页面，已经不能访问了，但其他页面是可以访问的。

### 3.只对一个页面起作用

上面都是对所有路由起作用的，如果只想中间件对一个特殊页面起作用，也是可以的。只要去掉.global的后缀就是可以的。 

在middleware 文件夹下，新建一个页面，default.ts，并编写下面的代码。

```js
export default defineNuxtRouteMiddleware((to, from) => {
  console.log("Hello")
})
```
这时候它对任何页面都是不起作用的，你需要再去对应的页面里注册一下。去pages文件夹，新建一个文件demo7.vue。然后需要注册这个页面使用这个中间件，代码如下。
```js
<template>
  <div class="">Demo7 Page</div>
</template>
<script setup>
definePageMeta({
  middleware: ["default"],
  // or middleware: 'auth'
});
</script>
<style scoped></style>
```
这样就对这个页面注册了一个专属的导航中间件。


## 十三、补充-Nuxt3 安装失败的时候如何处理

今天我重新安装了公司的系统，系统安装完成后，准备再安装Nuxt3新目录，发现Nuxt3在挂了代理的情况下，依然无法安装成功，会出现下面的错误。

**npx nuxi init nuxt-app**

```shell
D:\Demo>npx nuxi init nuxt-app
npm WARN config global `--global`, `--local` are deprecated. Use `--location=global` instead.
Need to install the following packages:
  nuxi
Ok to proceed? (y) y
Nuxt CLI v3.0.0-27398533.8edd481 
 WARN  could not fetch remote https://github.com/nuxt/starter                          
 WARN  Make sure you have installed git correctly
```

* 下载Nuxt3的文件包
在多次尝试失败的情况下，我决定先去Github打包下载Nuxt的基本文件，然后再用yarn命令进行安装。

于是我再Nuxt3的官方Github上找到了这样的网址。

https://github.com/nuxt/starter/tree/v3
打开网址可以看到，这个就是最简单的Nuxt3项目的目录，这时候你可以Clone下来，但我发现Clone还是会报错，意思是无法找到仓库位置。那这时候我只能用最原始的下载ZIP（Download ZIP）的方式了。

下载完成后，再使用yarn命令进行安装。

* yarn install

稍等一会，就可以安装成功了。安装成功以后，再使用

* yarn dev

开启服务后，再浏览器中输入 http://localhost:3000/ ,就可以看到结果了。 这样我们就解决了无法用官方给出的方法安装的问题了。本视频只是个补充视频，希望可以帮助到安装失败的用户，进行安装。

## 十四、Nuxt3 中SEO相关的配置

使用Nuxt3框架解决的主要问题就是要对搜索引擎友好,那为什么搜索引擎可以搜到我的网站那？这要归功于HTML中的Mate标签和title 标签。

title 和 meta 标签的作用

title标签：主要是为了告诉搜索引擎我们的网站标题是什么，然后搜索引擎才会根据你提供的的title给你打上tag，用户在搜索的时候才会搜索到你。

meta标签：这个标签根据name的不同有很多中，和SEO相关的主要是name=description 和name=keywords 这两种，如果不设置这两个标签，对SEO的效果就会有所影响。 

所以我们在开发需要SEO的网站时，对这两个标签一定要进行设置。当然你可以用两种方法对meta标签进行设置，

这节我们就讲两个方法。 1.使用useHead( )方法 2.直接在模板中使用标签

Nuxt3中的useHead 和useMeta

Nuxt3中提供了 useHead方法来设置SEO需要的内容，用它可以设置HTML中Head的全部内容，所以这也包括meta标签的内容，基本的使用方法也是很简单。

在根目录中下的 page文件夹下，新建一个文件`demo1.vue`，然后使用 useHead( )方法来设置头部信息。

```js
<template>
  <div class="">Demo8 Page</div>
</template>
<script setup>
useHead({
  title: " JSPang.com 技术胖的博客",
  viewport: "width=device-width,initial-scale=1,maximum-scale=1 ",
  charset: "utf-8",
  meta: [
    { name: "description", content: "技术胖的前端免费视频博客" },
    { name: "keywords", content: "技术胖" },
  ],
});
</script>
<style scoped></style>
```

如果你这时候报错，说明你按照的不是最新的Nuxt版本，可以直接安装最新的版本，我这里就在最新的版本上使用了useHead( ) 方法。

使用template中的标签定义Head

除了使用useHead( ) 方法外，你还可以直接使用<template> 中的的<head>来定义SEO相关的属性。

我们在/pages 文件夹下面，新建一个demo1.vue 的文件，然后编写下面的代码。

```js
<template>
  <div class="">
    <Head>
      <Title>{{ title }}</Title>
      <Meta name="description" :content="title" />
    </Head>
    <div>技术胖的博客</div>
  </div>
</template>
<script setup>
import { ref } from "vue";
const title = ref("技术胖的博客");
</script>
<style scoped></style>
```

从代码中可以看到，我们直接使用了<Head>标签，然后在里边还可以使用<Title>标签和<Meta>标签，可以设置这两个标签后，关于SEO的设置就都可以作了。

 我们使用Nuxt的意义就在于可以有很好的SEO效果，所以在你开发的时候，一定要对页面进行标题、描述和关键词的设置和编写。 

## 十五、Nuxt3中Cookie的设置

在网页制作时，经常需要临时保存一些信息到Cookie中，而不是全部都保存到数据库中，这样作能减轻服务器的压力。这节就学习一下Nuxt3中的Cookie操作。

### 1.cookie的作用

先来了解一下Cookie的作用，Cookie最常见的开发作用就是临时记录用户个人信息，比如我们登录了一个网站，然后提醒下次记住信息，下次再浏览这个网站时，就不用登录了。

这就是cookie起的作用，当我们登录一次后，把登录信息记录在了cookie里，但是这个记录是有时效性的，通过属性可以进行设置。比如你连续7天没登录，那cookie就过期了，再浏览这个网站就需要重新登录了。

### 2.useCookie( )方法的使用
```js
const cookie = useCookie(name, options)
```
制作登录太复杂，我们这属于是入门的教程，所以就用Cookie制作一个计数器，让你了解Cookie的使用方法。这里要使用的函数就是useCookie ,代码如下。
在pages 文件夹下，新建一个页面demo3.vue
```js
<template>
  <h1>Counter:{{ counter }}</h1>
  <button @click="reset">Reset</button>
  <button @click="add">Add</button>
</template>
<script setup>
const counter = useCookie("counter");
counter.value = counter.value || 0;
const reset = () => {
  counter.value = 0;
};
const add = () => {
  counter.value = counter.value + 1;
};
</script>
<style scoped></style>
```

这段代码的意思，我创建了一个叫做counter的Cookie值，然后取得Cookie值，放到页面上，如果没有Cookie值的时候，就初始化Counter的Cookie值为0。然后我又作了两个按钮，一个是直接将Cookie值设置为0，一个是每点击一次Cookie加1。
代码编写完成后，可以到浏览器中查看一下效果，你也可以按F12打开浏览器的调试模式，找到Application 标签，再找到Cookie 选项，就可以看到里边的Cookie值了，这也很好的证明我们的Cookie值设置成功了。

常用的相关属性
useCookie( )函数，第一个参数是设置Cookie值的名字，第二个参数为选项option,我们接着来看有那些可选择配置的Cookie参数。（注意：我这里只说两个常用的）

maxAge/expires

这两个参数都是设置Cookie的有效时长的，如果两个参数你都不设置，那Cookie的值在关闭浏览器的时候将会被清空。两个参数的不同是，maxAge的值是一个数字Number,而expires的值是一个日期对象Date object.
比如我们希望设置Cookie的过气时间是一个小时，也就是3600秒，那我们的配置就需要这样写。

const counter = useCookie("counter",{
  maxAge:3600,
});
2. httpOnly
这算是一个安全设置，如果把httpOnly设置为true，可以对最常见的XSS攻击起到防范作用。

什么是HttpOnly？ HttpOnly是包含在http返回头Set-Cookiew里面的一个附件的flag，所以它是后端服务器对cookie设置的一个附件属性，在生成cookie时使用HttpOnly标志有助于减轻客户端脚本访问收保护cookie的风险。

const counter = useCookie("counter",{
  htttpOnly:true,
});

3. secure
这也是一个安全设置，如果你的网址不是HTTPS的，并且把secure的值设置为true，那Cookie的值就不会传递给服务端。总的来说还是一个为了服务器安全的设置。

const counter = useCookie("counter",{
  secure:true,
});
这个需要配置HTTPS 所以不太好演示，这里也就不演示了。
其余的还有domain ,path ,sameSite ,encode,decode 这些属性设置，其实都跟安全有关，因为Cookie的设置确实需要考虑安全性，所以根据服务端和app的需求，尽量设置多的安全性参数
