<!--
 * @Author: your name
 * @Date: 2021-07-29 16:29:24
 * @LastEditTime: 2021-07-29 21:34:36
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \todo\src\components\TodoHeader.vue
-->
<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox" />
    </label>
    <span>
      <span>已完成</span>
    </span>
    <button class="btn btn-danger">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "TodoFooter",
};
</script>

<style>
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}
.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}
.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}
.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>
