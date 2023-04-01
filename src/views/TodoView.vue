<script setup>
import { ref, computed, watch } from "vue";
import { Icon } from "@iconify/vue";
import { uid } from "uid";
import Create from "../components/Create.vue";
import Item from "../components/Item.vue";

const todoList = ref([]);

const fetchTodoList = () => {
  const savedTodoList = JSON.parse(localStorage.getItem("todoList"));
  if (savedTodoList) {
    todoList.value = savedTodoList;
  }
};
// Fetch Todo's on page load
fetchTodoList();

const setTodoListLocalStorage = () => {
  localStorage.setItem("todoList", JSON.stringify(todoList.value));
};

watch(todoList, setTodoListLocalStorage, {
  deep: true,
});

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: false,
    isEditting: false,
  });
};
const toggleCheck = (index) => {
  todoList.value[index].isCompleted = !todoList.value[index].isCompleted;
};
const toggleEdit = (index) => {
  todoList.value[index].isEditting = !todoList.value[index].isEditting;
};
const deleteTodo = (todoId) => {
  todoList.value = todoList.value.filter((todo) => todo.id !== todoId);
};
const updateTodo = (e, index) => {
  todoList.value[index].todo = e;
};
const todosCompleted = computed(() => {
  return todoList.value.every((todo) => todo.isCompleted);
});
</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <Create @create-todo="createTodo" />
    <ul class="todo-list" v-if="todoList.length > 0">
      <Item
        v-for="(todo, index) in todoList"
        :todo="todo"
        :index="index"
        @check="toggleCheck"
        @edit="toggleEdit"
        @update="updateTodo"
        @delete="deleteTodo"
      />
    </ul>
    <p v-else class="todos-msg">
      <Icon icon="noto-v1:sad-but-relieved-face" />
      <span>You have no todo's to complete! Add one!</span>
    </p>
    <p v-if="todosCompleted && todoList.length > 0" class="todos-msg">
      <Icon icon="noto-v1:party-popper" />
      <span>You have completed all your todos!</span>
    </p>
  </main>
</template>

<style lang="scss" scoped>
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;
  h1 {
    margin-bottom: 16px;
    text-align: center;
  }
  .todo-list {
    display: flex;
    flex-direction: column;
    margin-top: 24px;
    gap: 20px;
  }
  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
}
</style>
