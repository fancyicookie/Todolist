<!--
 * @Date: 2022-11-26 15:49:55
 * @Author: Fancyicookie
-->
<template>
    <li class="item-checkbox">
        <label class="check"> 
            <input 
              class="checkbox" 
              type="checkbox" 
              :checked="todo.done" 
              @change="handleCheck(todo.id)" 
            >
            <!-- v-model的写法也行，但有些问题 -->
            <!-- <input class="checkbox" type="checkbox" v-model="todo.done" /> -->
            <span class="item">{{ todo.title }}</span>
        </label>
        <button class="btn" @click="handleDelete(todo.id)">删除</button>
    </li>
  
</template>

<script>
export default {
    name: 'MyItem',
    // 父向子传值，子接收 声明接收，props
    props:[ 'todo','checkTodo','deleteTodo' ],
    data() {
      return {   
      }
    },
    methods: {
      // 勾选or取消勾选
      handleCheck(id) {
          // 告诉app组件将对应的done值取反
        this.checkTodo(id);
      },
      // 删除
      handleDelete(id) {
        if(confirm('确定删除吗？')){
          this.deleteTodo(id)
        }
      }
    }
}
</script>
    
<style scoped>
  li {
    display: flex;
    align-items: center;
    list-style: none;
    margin-left: -40px;
    background-color: rgba(255, 255, 255, 0.418);
    border-bottom: 1px solid black;
    border-radius: 5px;
    font-size: 18px;
    font-family:'Times New Roman', Times, serif;
    height: 50px;
    width: 300px;
    color: rgb(148, 112, 151);
    /* box-shadow: 1px 1px 10px 1px; */
  }
  .checkbox {
    flex: 1;
    width: 22px;
    height: 22px;
    /* 解决checkbox与文本span的高度偏移问题*/
    vertical-align: top;
    margin-left: 20px;
    margin-right: 10px;
    font-family: 'Times New Roman', Times, serif;
  }
  .item {
    vertical-align: middle;
    background-color: rgba(255, 255, 255, 0.377);
  }
  .btn {
    border: 0;
    display: flex;
    display: none;
    justify-content: flex-end;
    border-radius: 5px;
  }
  .check {
    margin-right: 150px;
  }
  li:hover {
    background-color: rgb(239, 238, 240);
  }
  li:hover label {
    background-color: rgb(239, 238, 240);
  }
  li:hover button {
    display: block;
  }
</style>