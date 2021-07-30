<!--
 * @Author: your name
 * @Date: 2021-07-29 15:14:41
 * @LastEditTime: 2021-07-30 23:51:15
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \todo\src\App.vue
-->
<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <TodoHeader :addTodo="addTodo"></TodoHeader>
        <TodoList
          :todos="todos"
          :checkTodo="checkTodo"
          :deleteTodo="deleteTodo"
        ></TodoList>
        <TodoFooter
          :todos="todos"
          :allCheck="allCheck"
          :clearCheck="clearCheck"
        ></TodoFooter>
      </div>
    </div>
  </div>
</template>

<script>
//导入组件
import TodoHeader from "./components/TodoHeader.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";
import { nanoid } from "nanoid";
export default {
  name: "App",
  data() {
    return {
      todos: [
        { id: "001", title: "吃饭", completed: true },
        { id: "002", title: "学习", completed: false },
        { id: "003", title: "睡觉", completed: true },
      ],
    };
  },
  //组件注册
  components: { TodoHeader, TodoList, TodoFooter },
  methods: {
    //将函数传入子组件1 获取数据
    //将数据整理插入后再传入至子组件2
    addTodo(e) {
      if (!e.target.value) return alert("输入不能为空");
      const todoObj = { id: nanoid(), title: e.target.value, completed: false };
      this.todos.unshift(todoObj);
      e.target.value = "";
    },
    //切换值的动态响应
    checkTodo(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) todo.completed = !todo.completed;
      });
    },
    //删除一个代办事项
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    //全选
    allCheck(completed) {
      this.todos.forEach((todo) => {
        todo.completed = completed;
      });
    },
    //删除已选中事项
    clearCheck() {
      this.todos = this.todos.filter((todo) => !todo.completed);
    },
  },
};
</script>

<style>
body {
  background-color: #fff;
}
.todo-container {
  width: 600px;
  margin: 0 auto;
  box-shadow: 0 0 5px gray;
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
