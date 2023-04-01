<script setup>
import { reactive } from "vue";

const emit = defineEmits(["create-todo"]);
const todo = reactive({
  todo: "",
  invalid: false,
  errMsg: "Todo value cannot be empty!",
});

const create = () => {
  todo.invalid = false;
  if (todo.todo == "") {
    return (todo.invalid = true);
  }
  emit("create-todo", todo.todo);
  todo.todo = "";
};
</script>

<template>
  <main>
    <input type="text" v-model="todo.todo" />
    <button @click="create">Create</button>
  </main>
  <p class="err-msg" v-if="todo.invalid">{{ todo.errMsg }}</p>
</template>

<style lang="scss" scoped>
main {
  display: flex;
  transition: 250ms ease;
  border: 2px solid #41b080;
  &.input-err {
    border-color: red;
  }
  &:focus-within {
    box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
      0 -2px 4px -2px rgb(0 0 0 / 0.1);
  }
  input {
    width: 100%;
    padding: 8px 6px;
    border: none;
    &:focus {
      outline: none;
    }
  }
  button {
    padding: 8px 16px;
    border: none;
  }
}
.err-msg {
  margin-top: 6px;
  font-size: 12px;
  text-align: center;
  color: red;
}
</style>
