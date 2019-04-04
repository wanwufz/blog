---
title: vuejs组件的v-model使用示例
date: 2019-04-04 10:22:31
---
### 前言
  工作中总会忘记一些不常使用的技能，所谓好记性不如烂笔头，还是决定记录下这些看起来不太重要，用起来异常舒服的小知识点。

### 实例
  1. 首先要了解v-model的工作原理，[官网](https://cn.vuejs.org/v2/guide/components-custom-events.html#%E8%87%AA%E5%AE%9A%E4%B9%89%E7%BB%84%E4%BB%B6%E7%9A%84-v-model)解释为默认的prop与input事件，用以避免占用原生表单的value特性。
  2. 所以关键点就在默认的prop和默认的事件。可以通过以下例子更好的理解
    ```html
    <!-- 父组件里调用 -->
    <my-component v-model="name"></my-component>
    ```
    ```javascript
    export default{ // 子组件
      props:['value'], // 默认prop的key一般为value
      methods: {
        val_change(val){ // 监听组件内部数据的变化，同步到输入事件
          this.$emit('input', val) 
        }
      }
    }
    ```
  3. 从上面可以看出，v-model功能就是一个便捷版的父子组件通信功能。之所以看起来特别，就像官方所说：避免占用原生表单的事件和属性。

### 用处
  如果v-model就像上面理解的那样的话，总会让人觉得多此一举。其实它更多的用于复杂的子组件与父组件交互。比方说父组件传递了一个值进去，而子组件接收时会有很多计算或过滤来设置内部状态。每次更新这个值时实际上就是把组件内部传递给父组件。
  说起来比较绕，我在项目中一般用在文件上传，数据预览一类的子组件。这样可以把这些组件无缝对接elementui的表单验证。