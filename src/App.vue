<!--
 * @Author: your name
 * @Date: 2021-07-29 15:14:41
 * @LastEditTime: 2021-07-29 21:32:42
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \todo\src\App.vue
-->
<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <TodoHeader></TodoHeader>
        <TodoList></TodoList>
        <TodoFooter></TodoFooter>
      </div>
    </div>
  </div>
</template>

<script>
//导入组件
import TodoHeader from "./components/TodoHeader.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";
export default {
  name: "App",
  //组件注册
  components: { TodoHeader, TodoList, TodoFooter },
};
</script>

<style>
body {
  background-color: #fff;
}
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}
.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}
.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}
.btn:focus {
  outline: none;
}
</style>
