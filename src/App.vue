<!--
 * @Date: 2022-11-26 15:48:44
 * @Author: Fancyicookie
-->
<template>
  <div id="app">
    <h1>TODOS</h1>
    <hr style="width: 300px; margin-bottom: 30px"/>
    <!-- 如何将子组件的数据传递给父组件 -->
    <MyHeader :addTodo="addTodo" />
    <MyList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo" />
    <MyFooter :todos="todos" :checkAllTodo="checkAllTodo" :clearAllTodo="clearAllTodo"/>
  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue'
import MyList from './components/MyList.vue'
import MyFooter from './components/MyFooter.vue'
export default {
  name: 'App',
  components: {
    MyHeader,
    MyList,
    MyFooter
  },
  data() {
      return {
        todos: JSON.parse(localStorage.getItem('todos')) || []
      }
    },
    // 在js中，函数也是对象，传函数本身实际上是引用传递，意思是他们用的是同一块内存空间，一方修改，另一方也会改变
    // 父组件APP传递了一个函数给子组件MyHeader
  methods: {
    addTodo(todoObj){
      // console.log(x);
      this.todos.unshift(todoObj)
    },
    // 勾选/取消一个todo
    checkTodo(id) {
      this.todos.forEach((todo)=>{
        if(todo.id === id) todo.done = !todo.done
      })
    },
    // 删除一个Todo
    deleteTodo(id) {
      this.todos = this.todos.filter((todo)=>{
        return todo.id !== id
      })
    },
    // 全选or取消全选
    checkAllTodo(done) {
      this.todos.forEach(todo=>{
        todo.done = done
      })
    },
    // 清除所有已完成的todo
    clearAllTodo() {
      this.todos = this.todos.filter((todo)=>{
        return !todo.done
      })
    }

  },
  watch: {
    todos: {
      deep: true,
      // localStorage.setItem('todos', JSON.stringify(value)) // bug 监测不到数组里面的变化
      handler(value) {
        localStorage.setItem('todos', JSON.stringify(value))
      }
    }
  }
}
</script>

<style lang="less">
* {
  background-color: rgba(241, 238, 241, 0.795);
}
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h1 {
  margin-bottom: 10px;
  font-size: 60px;
  color: #c2a9ca;
}
label {
  background-color: rgba(255, 255, 255, 0.418);
}
</style>
