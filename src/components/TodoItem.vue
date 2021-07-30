<!--
 * @Author: your name
 * @Date: 2021-07-29 16:29:24
 * @LastEditTime: 2021-07-30 20:41:38
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \todo\src\components\TodoHeader.vue
-->
<template>
  <li>
    <label>
      <input
        type="checkbox"
        :checked="things.completed"
        @change="handleCheck(things.id)"
      />
      <!-- 双向绑定修改props中的数据 实现修改checked的布尔值 -->
      <!-- <input
        type="checkbox"
        :checked="things.completed"
        v-model="things.completed"
      /> -->
      <span>{{ things.title }}</span>
    </label>
    <button class="btn btn-danger" @click="deleteBtn(things.id)">删除</button>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["things", "checkTodo", "deleteTodo"],
  methods: {
    //标记todo的id 传入到从父级层层传递来的处理方法
    handleCheck(id) {
      this.checkTodo(id);
    },
    deleteBtn(id) {
      if (confirm("确定删除")) {
        this.deleteTodo(id);
      }
    },
  },
};
</script>

<style scoped>
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}
li label {
  float: left;
  cursor: pointer;
}
li label span {
  margin-left: 10px;
}
/* li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
} */
li button {
  float: right;
  display: none;
  margin-top: 3px;
}
li:before {
  content: initial;
}
li:last-child {
  border-bottom: none;
}
li:hover {
  background-color: #ddd;
}
li:hover button {
  display: block;
}
</style>
