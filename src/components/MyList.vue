<!--
 * @Date: 2022-11-26 15:49:55
 * @Author: Fancyicookie
-->
<template>
  <ul>
    <MyItem 
      v-for="todoObj in todos" 
      :key="todoObj.id" 
      :todo="todoObj"
      :checkTodo="checkTodo" 
      :deleteTodo="deleteTodo"
    />
  </ul>
</template>

<script>
import MyItem from './MyItem.vue'
export default {
    name: 'MyList',
    components: { MyItem },
    props: ['todos', 'checkTodo','deleteTodo'],
    methods: {
      
    }
}
</script>

<style>

</style>