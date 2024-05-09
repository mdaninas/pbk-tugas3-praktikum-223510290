<script setup>
import { ref, computed } from "vue";

let id = 0;

const newTodo = ref("");
const hideCompleted = ref(false);
const todos = ref([
  { id: id++, text: "Tugas DAA", done: true },
  { id: id++, text: "Tugas PBO", done: true },
  { id: id++, text: "Tugas PBK", done: false },
]);

const filteredTodos = computed(() => {
  return hideCompleted.value ? todos.value.filter((t) => !t.done) : todos.value;
});

const editingTodoId = ref(null);

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false });
  newTodo.value = "";
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo);
}

function startEditing(todo) {
  editingTodoId.value = todo.id;
}

function updateTodoText(todo) {
  editingTodoId.value = null;
}

function cancelEditing() {
  editingTodoId.value = null;
}
</script>

<template>
  <div class="main">
    <div class="main2">
      <div class="isi1">
      <h1>Todolist ku</h1>
      <form @submit.prevent="addTodo">
        <input v-model="newTodo" required placeholder="new todo" />
        <button class="buttonch">Add Todo</button>
      </form>
      </div>
      <div class="isi2">
      
      <ul>
        <li v-for="todo in filteredTodos" :key="todo.id">
          <div class="list">
          <span class="check">
          <input type="checkbox" v-model="todo.done" />
          <span v-if="editingTodoId !== todo.id" :class="{ done: todo.done }">{{
            todo.text
          }}</span>
          <input
            v-else
            type="text"
            v-model="todo.text"
            @keyup.enter="updateTodoText(todo)"
            @blur="cancelEditing"
          />
          </span>
          </div>
          <span class="buttoned">
          <button @click="removeTodo(todo)" class="buttonch">Remove</button>
          <button @click="startEditing(todo)" style="margin-left: 10px;margin-right: 10px;" class="buttonch">Edit</button>
          </span>
          
        </li>
      </ul>
      </div>
    </div>
  </div>
</template>

<style scoped>
input[type="checkbox"]{
  margin-right: 20px;
  scale: 2.5;
}

.done {
  text-decoration: line-through;
}
h1{
  font-family: "Poetsen One", sans-serif;
  font-weight: 400;
  font-style: normal;
  position: relative;
  bottom: 40px;
 font-size: 100px;
}
span{
  font-family: "Sedan SC", serif;
  font-weight: 400;
  font-style: normal;
  font-size:30px;
}
li {
  list-style-type: none;
  display:flex ;
  justify-content: space-between;
  gap: 40px;
}
form{
  display: flex;
  gap: 40px;
  justify-content: space-around;
}
span.check{
  gap: 20px;
}
.main2{
  background: rgba(255, 255, 255, 0.5);
  backdrop-filter: blur(2px);
  position: relative;
  height: 80%;
  width: 80%;
  border-radius: 40px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}
.isi1{
  text-align: center;
 
  display: flex;
  flex-direction: column;
}
span.check{
  margin-left: 20px; /* Tambahkan margin kiri di sini */
}
.list{
  margin-bottom: 40px;
}
.isi2{
justify-content: space-between;
width: 80%;
height: 40%;
overflow: auto;
}

.main {
  background-color: black;
  height: 100vh;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background-image: url(./assets/bg.gif);
}

.buttonch {
  background-color: #222;
  border-radius: 4px;
  border-style: none;
  box-sizing: border-box;
  color: #fff;
  cursor: pointer;
  display: inline-block;
  font-family: "Farfetch Basis","Helvetica Neue",Arial,sans-serif;
  font-size: 16px;
  font-weight: 700;
  line-height: 1.5;
  margin: 0;
  max-width: none;
  outline: none;
  overflow: hidden;
  position: relative;
  text-align: center;
  text-transform: none;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  padding: 10PX;
}

.buttonch:hover,
.buttonch:focus {
  opacity: .75;
}
</style>
