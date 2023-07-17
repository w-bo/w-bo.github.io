---
title: vue-插槽的使用
date: 2023-07-13 14:57:32
tags:
categories:
---

# 什么是插槽？

## 简单介绍一下

### 概念

插槽（Slots）是Vue.js中的一个重要概念，用于在组件中定义可插入内容的位置。它允许您在组件外部传递内容到组件内部，以实现更灵活的组件复用和组合。

使用插槽，您可以在组件的模板中预留一些区域，然后在使用该组件时，通过插槽将内容传递进来。这样，您可以根据需要定制组件的部分或全部内容。

<!-- more -->

### 用法

下面是一个示例，展示了如何在Vue.js组件中使用插槽：

```html
<!-- 父组件模板 -->
<template>
  <div>
    <child-component>
      <p>这是父组件中的内容</p>
    </child-component>
  </div>
</template>

<!-- 子组件模板 -->
<template>
  <div>
    <slot></slot>
  </div>
</template>
```

在上面的例子中，父组件使用`<child-component>`标签包裹了一段内容`<p>这是父组件中的内容</p>`。这段内容将会被传递到子组件中。

子组件中的`<slot></slot>`表示一个插槽，它标志着子组件的模板中的一个插入点。在使用子组件时，插入到这个插槽中的内容将会被显示。

当父组件渲染时，子组件的插槽会将父组件传递的内容进行渲染，使得父组件中的内容可以动态地嵌入到子组件中。

此外，您还可以为插槽提供默认内容，当没有传递内容时将会显示该默认内容。可以通过在子组件中使用`<slot>默认内容</slot>`的方式定义默认内容。

除了默认插槽之外，Vue.js还支持具名插槽和作用域插槽等更高级的插槽用法，使得插槽更加灵活和功能强大。但以上介绍的是插槽的基本用法，您可以根据需要进行更进一步的学习和实践。

tips：值得注意的是

> 在 2.6.0 中，我们为具名插槽和作用域插槽引入了一个新的统一的语法 (即 `v-slot` 指令)。它取代了 `slot` 和 `slot-scope` 这两个目前已被废弃但未被移除且仍在[文档中](https://v2.cn.vuejs.org/v2/guide/components-slots.html#%E5%BA%9F%E5%BC%83%E4%BA%86%E7%9A%84%E8%AF%AD%E6%B3%95)的 attribute。新语法的由来可查阅这份 [RFC](https://github.com/vuejs/rfcs/blob/master/active-rfcs/0001-new-slot-syntax.md)。



## 插槽的分类

除了基本的插槽用法，Vue.js还提供了一些高级的插槽用法，包括具名插槽和作用域插槽。这些高级用法可以让您更加灵活地控制插槽内容的渲染和数据传递。

### 具名插槽

具名插槽（Named Slots）：
具名插槽允许您在组件中定义多个插槽，并为每个插槽命名，以便更细粒度地控制插槽内容的插入位置。使用具名插槽，您可以在父组件中指定要插入到特定插槽位置的内容。

#### 示例

```html
<!-- 子组件模板 -->
<template>
  <div>
    <slot name="header"></slot>
    <slot name="content"></slot>
    <slot name="footer"></slot>
  </div>
</template>

<!-- 父组件模板 -->
<template>
  <div>
    <child-component>
      <template v-slot:header>
        <h1>这是头部内容</h1>
      </template>
      <template v-slot:content>
        <p>这是主要内容</p>
      </template>
      <template v-slot:footer>
        <footer>这是底部内容</footer>
      </template>
    </child-component>
  </div>
</template>
```

在上面的例子中，子组件中定义了三个具名插槽，分别是`header`、`content`和`footer`。在父组件中使用`v-slot`指令指定要插入到相应插槽的内容。

### 作用域插槽

作用域插槽（Scoped Slots）：
作用域插槽允许您向插槽内容传递数据，并在父组件中使用该数据进行渲染。这样，您可以在父组件中对插槽内容进行更加细粒度的控制。

以下是一个更具体的示例，展示了如何使用作用域插槽来自定义列表组件的渲染逻辑。

#### 示例

```html
<!-- 子组件模板 -->
<template>
  <div>
    <ul>
      <li v-for="item in items">
        <slot :item="item">{{ item }}</slot>
      </li>
    </ul>
  </div>
</template>

<!-- 父组件模板 -->
<template>
  <div>
    <child-component>
      <template v-slot:item="slotProps">
        <span>{{ slotProps.item }}</span>
        <button @click="deleteItem(slotProps.item)">删除</button>
      </template>
    </child-component>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: ['苹果', '香蕉', '橙子']
    };
  },
  methods: {
    deleteItem(item) {
      const index = this.items.indexOf(item);
      if (index !== -1) {
        this.items.splice(index, 1);
      }
    }
  }
};
</script>
```

在这个示例中，子组件是一个简单的列表组件，它接受一个名为`items`的数组作为数据源。在子组件的模板中，使用`v-for`遍历`items`数组，并为每个项目创建一个`<li>`元素。通过作用域插槽，我们将当前的`item`作为数据传递给插槽，并在插槽内容中使用`{{ item }}`来渲染项目的文本内容。

在父组件中，我们使用`child-component`来包裹列表组件，并在父组件的模板中使用作用域插槽来自定义每个列表项的渲染方式。在这个例子中，我们为每个列表项显示了一个文本`<span>`，并附加了一个删除按钮。通过作用域插槽，我们可以访问到每个列表项的数据，并在插槽内容中使用这些数据进行渲染和交互。

父组件还定义了一个`deleteItem`方法，用于从列表中删除特定的项目。当点击删除按钮时，将调用该方法，并传递当前项目的数据作为参数。

通过这个示例，您可以看到作用域插槽的强大之处。它使父组件能够对子组件的渲染逻辑进行更精细的控制，并且可以在插槽内容中与子组件进行交互。您可以根据实际需求使用作用域插槽来实现更复杂的自定义组件行为。

以上是插槽的一些高级用法，您可以根据需要使用具名插槽和作用域插槽来实现更灵活和可复用的组件。



## 插槽的动态用法

插槽（Slots）在Vue.js中具有灵活的动态用法，您可以根据需要动态地定义和使用插槽。

以下是一些插槽的动态用法示例：

1. 动态传递插槽名称、内容：

   在Vue.js中，v-slot指令可以与动态值进行绑定。这使得您可以在父组件中动态地确定要传递给子组件的插槽内容。

   下面是一个示例，展示了如何在父组件中使用动态值绑定v-slot：

   父组件模板：

   ```html
   <template>
     <div>
       <child-component>
         <template v-slot:[slotName]="slotProps">
           <p>父组件传递的值为: {{ slotProps.value }}</p>
         </template>
       </child-component>
     </div>
   </template>
   
   <script>
   export default {
     data() {
       return {
         slotName: 'default',
       }
     }
   }
   </script>
   ```

   

   子组件模板：

   ```html
   <template>
     <div>
       <slot :value="dynamicValue"></slot>
     </div>
   </template>
   
   <script>
   export default {
     data() {
       return {
         dynamicValue: '这是一个动态的值'
       }
     }
   }
   </script>
   ```

   在上面的例子中，父组件使用动态值绑定v-slot指令的名称部分。这里的`[slotName]`表示slotName是一个动态的变量，它的值由父组件的data属性中的`slotName`确定。

   子组件中的插槽使用相同的动态值作为其名称部分，以便正确接收来自父组件的插槽内容。

   这样，您可以根据需要在父组件中动态地指定要传递给子组件的插槽内容，通过在父组件中更新`slotName`的值来实现动态绑定。

