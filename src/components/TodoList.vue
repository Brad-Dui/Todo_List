<!--
 * @Author: your name
 * @Date: 2021-07-29 16:29:24
 * @LastEditTime: 2021-07-29 21:14:53
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \todo\src\components\TodoHeader.vue
-->
<template>
  <ul class="todo-main">
    <TodoItem></TodoItem>
  </ul>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
  name: "TodoList",
  components: { TodoItem },
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
