<script setup>
import { ref, reactive, defineEmits } from "vue";
import TodoButton from "./TodoButton.vue";
const todo = ref("");

const emit = defineEmits(["create-todo"]);

const todoState = reactive({
  todo: "",
  invalid: null,
  errMsg: "",
});

const createTodo = () => {
  todoState.invalid = null;
  if (todoState.todo != "") {
    emit("create-todo", todoState.todo);
    todoState.todo = "";
    return;
  }
  todoState.invalid = true;
  todoState.errMsg = "Todo value cannot be empty";
};
</script>
<template>
  <div class="wrapper">
    <div class="input-wrap" :class="{ 'input-err': todoState.invalid }">
      <input type="text" placeholder="New Todo" v-model="todoState.todo" />
      <TodoButton @click="createTodo()"> Create </TodoButton>
    </div>

    <p v-show="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p>
  </div>
</template>

<style lang="scss" scoped>
.wrapper {
  .err-msg {
    margin: 8px 0;
    color: red;
    font-size: 14px;
  }
  .input-wrap {
    display: flex;
    transition: 250ms ease;
    border: lightblue solid 1px;
    &:focus-within {
      border: 1px solid rgb(27, 126, 192);
    }
    &.input-err {
      border-color: red;
      button {
        background-color: rgb(242, 241, 241);
        &:hover {
          background-color: rgb(242, 241, 241);
        }
      }
    }

    input {
      width: 100%;
      padding: 8px 6px;
      border: none;
      &:focus {
        outline: none;
      }
    }
  }
}
</style>
