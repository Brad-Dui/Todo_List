<!--
 * @Author: your name
 * @Date: 2021-07-29 16:29:24
 * @LastEditTime: 2021-07-30 23:49:21
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \todo\src\components\TodoHeader.vue
-->
<template>
  <div class="todo-footer" v-show="all">
    <label>
      <input type="checkbox" v-model="isAll" />
    </label>
    <span>
      <span>已完成{{ completedTotal }} / 全部{{ all }}</span>
    </span>
    <button class="btn btn-danger" @click="clear">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "TodoFooter",
  props: ["todos", "allCheck", "clearCheck"],
  methods: {
    clear() {
      this.clearCheck();
    },
  },
  computed: {
    all() {
      return this.todos.length;
    },
    completedTotal() {
      //reduce条件筛选
      return this.todos.reduce(
        (pre, current) => pre + (current.completed ? 1 : 0),
        0
      );
    },
    isAll: {
      get() {
        return this.all === this.completedTotal && this.all > 0;
      },
      set(value) {
        this.allCheck(value);
      },
    },
  },
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
