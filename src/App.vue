
<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <TodoHeader @addTodo="addTodo"></TodoHeader>
        <TodoList :todos="todos"></TodoList>
        <TodoFooter
          :todos="todos"
          @allCheck="allCheck"
          @clearCheck="clearCheck"
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
import pubsub from "pubsub-js";
export default {
  name: "App",
  data() {
    return {
      todos: JSON.parse(localStorage.getItem("todos")) || [],
    };
  },
  //组件注册
  components: { TodoHeader, TodoList, TodoFooter },
  methods: {
    //将函数传入子组件1 获取数据
    //将数据整理插入后再传入至子组件2
    addTodo(todoObj) {
      this.todos.unshift(todoObj);
    },
    //切换值的动态响应
    checkTodo(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) todo.completed = !todo.completed;
      });
    },
    //删除一个代办事项
    deleteTodo(_, id) {
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
    //失去焦点更新
    updateData(id, title) {
      this.todos.forEach((todo) => {
        if (todo.id === id) todo.title = title;
      });
    },
  },
  mounted() {
    this.$bus.$on("checkTodo", this.checkTodo);
    //消息订阅
    this.pubid = pubsub.subscribe("deleteTodo", this.deleteTodo);
    //绑定更新
    this.$bus.$on("updateData", this.updateData);
  },
  beforeDestroy() {
    this.$bus.off("checkTodo");
    this.$bus.off("updateData");
    pubsub.unsubscribe(this.pubid);
  },
  watch: {
    todos: {
      deep: true,
      handler(value) {
        localStorage.setItem("todos", JSON.stringify(value));
      },
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
.btn-edit {
  color: #fff;
  background-color: #2edef5;
  border: 1px solid #1fc9f3;
  margin-right: 5px;
}
.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}
.btn-edit:hover {
  color: #fff;
  background-color: #1fc9f3;
}
.btn:focus {
  outline: none;
}
</style>
