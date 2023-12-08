<script setup lang="ts">
import { TodoStatus } from "@/types";
import Draggable from "vuedraggable";
import useTodos from "@/store/useTodos";
import CreateTodo from "./CreateTodo.vue";

interface Props {
  status: TodoStatus;
}

const props = defineProps<Props>();

const { getTodosByStatus, deleteTodo, updateTodo } = useTodos();
const todoList = getTodosByStatus(props.status);

const groupLabel = {
  [TodoStatus.Pending]: "Pending",
  [TodoStatus.InProgress]: "In Progress",
  [TodoStatus.Completed]: "Completed",
};

const onDraggableChange = (payload: any) => {
  if (payload?.added?.element?.status) {
    updateTodo(payload?.added?.element, props.status);
  }
};
</script>

<template>
  <div class="group-wrapper">
    <h3>{{ groupLabel[props.status] }}</h3>
    <Draggable
      class="draggable"
      :list="todoList"
      group="todos"
      itemKey="id"
      @change="onDraggableChange"
    >
      <template #item="{ element: todo }">
        <li>
          {{ todo.title }}
          <span class="delete-icon" @click="deleteTodo(todo)">x</span>
          <div>
            <span class="todo-description">{{ todo.description }}</span>
          </div>
        </li>
      </template>
    </Draggable>

    <CreateTodo :status="props.status" />
  </div>
</template>

<style lang="scss" scoped>

.group-wrapper {
  flex: 1;
  padding: 20px;
  background-color: transparent;
  border: 1px solid #8d8d8d;
  width: 300px;
  border-radius: 15px;
  h3 {
    color: #1a1a1a;
    font-size: 22px;
  }

  li {
    border-radius: 10px;
    list-style-type: none;
    background-color: #dbdbdb;
    color: rgb(0, 0, 0);
    padding: 10px;
    cursor: grab;
    margin-bottom: 10px;
  }

  .draggable {
    min-height: 200px;
  }

  .delete-icon {
    float: right;
    cursor: pointer;
    margin-top: 5px;
    font-weight: bold;
    font-size: 20px;
    color: red;
  }

  .todo-description {
    font-size: 12px;
  }
}
</style>
