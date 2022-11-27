<!--
 * @Date: 2022-11-26 15:49:55
 * @Author: Fancyicookie
-->
<template>
  <div class="header">
    <input class="head" type="text" placeholder="请输入任务：Enter确认" @keyup.enter="add">
  </div>
</template>

<script>
import { nanoid } from 'nanoid'
export default {
    name: 'MyHeader',
    // 父组件APP传递了一个函数，子组件调用函数receive需要参数
    props: ['addTodo'],
    methods: {
      add(e) {
        if(!e.target.value.trim()) return alert('输入不能为空')
        // 将输入包装成一个todo对象,主要问题为id如何唯一
        // console.log(e.target.value);
        const todoObj = { id: nanoid(), title: e.target.value, done: false}
        // 子组件调用这个函数把需要的值一起传递过去了
        this.addTodo(todoObj)
        // 清空输入
        e.target.value = ''
      }
    }
}
</script>

<style scoped>
  .header {
    background-color: rgb(255, 255, 255);
  }
  .head {
    background-color: rgb(255, 255, 255);
    border: 0px;
    border-radius: 5px;
    font-size: 20px;
    font-family:'Times New Roman', Times, serif;
    height: 50px;
    width: 300px;
    color: rgb(177, 179, 180);
    box-shadow: 1px 1px 10px 1px;
  }
</style>