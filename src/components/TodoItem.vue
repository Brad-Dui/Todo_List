<!--
 * @Author: your name
 * @Date: 2021-07-29 16:29:24
 * @LastEditTime: 2021-08-02 22:01:42
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
      <span v-show="!things.isEdit">{{ things.title }}</span>
      <input
        class="inputBlur"
        v-show="things.isEdit"
        type="text"
        :value="things.title"
        @blur="handleBlur(things, $event)"
        ref="inputBlur"
      />
    </label>
    <button class="btn btn-danger" @click="deleteBtn(things.id)">删除</button>
    <button
      v-show="!things.isEdit"
      class="btn btn-edit"
      @click="editBtn(things)"
    >
      编辑
    </button>
  </li>
</template>

<script>
import pubsub from "pubsub-js";
export default {
  name: "TodoItem",
  props: ["things"],
  methods: {
    //标记todo的id 传入到从父级层层传递来的处理方法
    handleCheck(id) {
      this.$bus.$emit("checkTodo", id);
    },
    deleteBtn(id) {
      if (confirm("确定删除")) {
        //消息发布
        pubsub.publish("deleteTodo", id);
      }
    },
    editBtn(things) {
      if (things.hasOwnProperty.call(things, "isEdit")) {
        things.isEdit = true;
      } else {
        this.$set(things, "isEdit", true);
      }
      this.$nextTick(function () {
        this.$refs.inputBlur.focus();
      });
    },
    handleBlur(things, e) {
      things.isEdit = false;
      if (!e.target.value.trim()) return alert("输入不能为空");
      this.$bus.$emit("updateData", things.id, e.target.value);
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
li .inputBlur:focus {
  outline: none;
  margin-left: 10px;
  height: 20px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 5px;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(82, 168, 236, 0.6);
}
</style>
