<script setup>
import { ref, watch, computed } from "vue";
import { uid } from "uid";
import TodoCreator from "../components/TodoCreator.vue";
import TodoItem from "../components/TodoItem.vue";
import { Icon } from "@iconify/vue";
const todoList = ref([]);

watch(
  todoList,
  (newValue, oldValue) => {
    setTodoListLocalStorage();
  },
  {
    deep: true,
  }
);
const todoCompleted = computed(() => {
  // every loops thru array and check if every is completed in array is true
  return todoList.value.every((todo) => todo.isCompleted);
});
const setTodoListLocalStorage = () => {
  localStorage.setItem("todoList", JSON.stringify(todoList.value));
};

const fetchTodoListLocalStorage = () => {
  const savedTodoList = JSON.parse(localStorage.getItem("todoList"));
  if (savedTodoList != null) {
    todoList.value = savedTodoList;
  }
};

fetchTodoListLocalStorage();

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null,
  });
};
const toggleTodoComplete = (index) => {
  if (
    todoList.value[index].isCompleted == false ||
    todoList.value[index].isCompleted == null
  ) {
    todoList.value[index].isCompleted = true;
  } else {
    todoList.value[index].isCompleted = false;
  }
  // todoCompleted();
  // todoList.value[index].isCompleted = !todoList.value[index].isCompleted;
};
const toggleEditTodo = (index) => {
  if (
    todoList.value[index].isEditing == false ||
    todoList.value[index].isEditing == null
  ) {
    todoList.value[index].isEditing = true;
  } else {
    todoList.value[index].isEditing = false;
  }

  // todoList.value[index].isEditing = !todoList.value[index].isEditing;
};
const updateTodo = (todoVal, index) => {
  todoList.value[index].todo = todoVal;
};
const deleteTodo = (todoId) => {
  todoList.value = todoList.value.filter((todo) => todo.id !== todoId);
};
</script>

<template>
  <div>
    <main>
      <h1>Create Todo</h1>

      <TodoCreator @create-todo="createTodo"></TodoCreator>
      <ul class="todo-list" v-if="todoList.length > 0">
        <TodoItem
          v-for="(todo, index) in todoList"
          :todo="todo"
          :index="index"
          @toggle-complete="toggleTodoComplete"
          @edit-todo="toggleEditTodo"
          @update-todo="updateTodo"
          @delete-todo="deleteTodo"
        >
        </TodoItem>
      </ul>
      <p class="todo-msg" v-else>
        <Icon icon="ph:smiley-sad" color="#1b7ec0" width="22" />
        <span>You have no todos to complete! Add one in!</span>
      </p>
      <p v-if="todoCompleted && todoList.length > 0" class="todo-msg">
        <Icon icon="ph:smiley" color="#1b7ec0" width="22" />

        <span>You have completed all of your todo!</span>
      </p>
    </main>
  </div>
</template>

<style lang="scss" scoped>
main {
  display: flex;
  flex-direction: column;
  width: 100%;
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
  h1 {
    display: flex;
    justify-content: center;
    margin: 24px 0px;
  }
  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }
  .todo-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
}
</style>
