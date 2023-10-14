<script setup>
import { defineEmits } from "vue";
defineEmits(["toggle-complete", "edit-todo", "update-todo", "delete-todo"]);

const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
  index: {
    type: Number,
    required: true,
  },
});

import { Icon } from "@iconify/vue";
</script>
<template>
  <li>
    <input
      type="checkbox"
      :checked="todo.isCompleted"
      @input="$emit('toggle-complete', index)"
    />

    <div class="todo">
      <input
        @input="$emit('update-todo', $event.target.value, index)"
        v-if="todo.isEditing"
        type="text"
        :value="todo.todo"
      />
      <span v-else :class="{ 'completed-todo': todo.isCompleted }">{{
        todo.todo
      }}</span>
    </div>
    <div class="todo-actions">
      <Icon
        v-if="todo.isEditing"
        icon="ph:check-circle"
        color="#1b7ec0"
        width="22"
        @click="$emit('edit-todo', index)"
      />
      <Icon
        v-else
        icon="ph:pencil"
        color="#1b7ec0"
        width="22"
        @click="$emit('edit-todo', index)"
      />
      <Icon
        icon="ph:trash"
        color="crimson"
        width="22"
        @click="$emit('delete-todo', todo.id)"
      />
    </div>
  </li>
</template>

<style lang="scss" scoped>
li {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 16px 10px;
  background-color: #f1f1f1;
  box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1),
    0 8px 10px -6px rgb(0 0 0 / 0.1);
  &:hover {
    .todo-actions {
      opacity: 1;
    }
  }

  input[type="checkbox"] {
    appearance: none;
    width: 20px;
    height: 20px;
    background-color: #fff;
    border-radius: 50px;
    box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
    &:checked {
      background-color: lightblue;
    }
  }
  .todo {
    flex: 1;
    input[type="text"] {
      width: 100%;
      padding: 2px 6px;
      border: 1px solid lightblue;
    }
    .completed-todo {
      text-decoration: line-through;
    }
  }
  .todo-actions {
    display: flex;
    gap: 6px;
    opacity: 0;
    transform: 250ms ease-in-out;
    .icon {
      cursor: pointer;
    }
  }
}
</style>
