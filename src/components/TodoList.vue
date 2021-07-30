<!--
 * @Author: your name
 * @Date: 2021-07-29 16:29:24
 * @LastEditTime: 2021-07-30 20:39:03
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \todo\src\components\TodoHeader.vue
-->
<template>
  <ul class="todo-main">
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :things="todo"
      :checkTodo="checkTodo"
      :deleteTodo="deleteTodo"
    ></TodoItem>
  </ul>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
  name: "TodoList",

  components: { TodoItem },
  props: ["todos", "checkTodo", "deleteTodo"],
};
</script>

<style scoped>
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}
</style>
