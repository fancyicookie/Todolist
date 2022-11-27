<!--
 * @Date: 2022-11-26 15:52:23
 * @Author: Fancyicookie
-->
<template>
  <div  class="footer" v-show="total">
    <label>
      <input type="checkbox" :checked="isAll" @change="checkAll">
      <span class="done">已完成 {{ doneTotal }} </span>
      <span> / 全部 {{ total }}</span>
    </label>
    <button @click="clearAll">删除已完成</button>
  </div>
</template>

<script>
export default {
    name: 'Footer',
    props: ['todos','checkAllTodo', 'clearAllTodo'],
    computed: {
      total() {
        return this.todos.length
      },
      doneTotal(){
        // this.todos.reduce((pre,current)=>{
        //   return pre + (current.done ? 1 :  0)
        // },0)
        return this.todos.reduce((pre,todo) => pre + (todo.done ? 1 : 0),0)
      },
      isAll() {
        return this.doneTotal === this.total && this.doneTotal > 0
      }
    },
    methods: {
      checkAll(e) {
        this.checkAllTodo(e.target.checked)
      },
      clearAll(){
        if(confirm('确定删除吗？')) {
          this.clearAllTodo()
        }
      }
    }
}
</script>

<style scoped>
.footer {
    display: flex;
    align-items: center;
    list-style: none;
    background-color: rgba(255, 255, 255, 0.438);
    border-radius: 5px;
    font-size: 16px;
    font-family:'Times New Roman', Times, serif;
    height: 50px;
    width: 350px;
    color: rgb(77, 126, 155);
    /* box-shadow: 1px 1px 10px 1px; */
  }
  .footer input {
    width: 22px;
    height: 22px;
    /* 解决checkbox与文本span的高度偏移问题*/
    vertical-align: middle;
    margin-left: 20px;
    margin-right: 10px;
    font-family: 'Times New Roman', Times, serif;
  }
  .footer span {
    vertical-align: middle;
    background-color: rgba(255, 255, 255, 0.418);
  }
  .footer button {
    border: 0;
    display: flex;
    justify-content: flex-end;
    margin-left: 70px;
    border-radius: 5px;
  }
</style>