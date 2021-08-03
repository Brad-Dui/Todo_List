<!--
 * @Author: your name
 * @Date: 2021-07-29 16:29:24
 * @LastEditTime: 2021-08-03 14:06:44
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \todo\src\components\TodoHeader.vue
-->
<template>
  <ul class="todo-main">
    <transition-group name="anmtTodo">
      <TodoItem v-for="todo in todos" :key="todo.id" :things="todo"></TodoItem>
    </transition-group>
  </ul>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
  name: "TodoList",

  components: { TodoItem },
  props: ["todos"],
};
</script>

<style scoped>
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
  overflow: hidden;
}
.anmtTodo-enter {
  transform: translateX(100%);
}
.anmtTodo-enter-to,
.anmtTodo-leave {
  transform: translateX(0);
}
.anmtTodo-leave-to {
  transform: translateX(-100%);
}
.anmtTodo-enter-active,
.anmtTodo-leave-active {
  transition: 0.5s linear;
}
</style>
