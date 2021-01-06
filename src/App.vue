<template>
<img alt="Vue logo" src="./assets/logo.png">
<h1>Vue 3 Todo App</h1>
  <form @submit.prevent="addNewTodo">
    <label><h3>new Todo</h3>
    <input placeholder="HERE!" v-model="newTodo" name="newTodo"><br>
    </label><br>
    <button class="button">Add new Todo</button>
  </form><br>
  <button class="button" @click="markAllDone">Mark All Done</button><br><br>
  <button class="button" @click="removeAll">Remove All</button>
  <!-- <h2>{{newTodo}}</h2> -->
<ul>
  <li v-for="(todo , index) in todos" :key="todo.id" class="todo">
      <h3 :class="{ done:todo.done }" @click="toggleDone(todo)">{{todo.content}}</h3>
      <button class="button" @click="removeTodo(index)">Remove Todo</button>
  </li>
  </ul>
  <br>
  <br>
  <br>
  <br>
  <br>
  <br>
  <br>
</template>

<script>
import { ref } from 'vue';

export default {
   setup(){

    //  const data = reactive({
    //    newTodo:'',
    //    todos:[],
    //  });
     const newTodo = ref('');
     const todos  = ref([]);

     function addNewTodo(){
      //  console.log('form was submitted');
      // console.log(newTodo.value);
      todos.value.push({
        id:Date.now(),
        done:false,
        content: newTodo.value,
      });
      newTodo.value = "";
     }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index,1)
    }

    function markAllDone(){
      todos.value.forEach((todo) => todo.done = true)
    }

    function removeAll(){
      todos.value = []
    }

     return{
       todos,
       newTodo,
       addNewTodo,
       toggleDone,
       removeTodo,
       markAllDone,
       removeAll,
     };
   }
}
</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #42b983;
  margin-top: 60px;
}

.done {
  text-decoration: line-through;
}

.todo{
  cursor: pointer;
}
.button {
  display: inline-block;
  padding: 15px 25px;
  font-size: 24px;
  cursor: pointer;
  text-align: center;
  text-decoration: none;
  outline: none;
  color: #fff;
  background-color: #42b983;;
  border: none;
  border-radius: 15px;
  box-shadow: 0 9px #999;
}

.button:hover {background-color: #3e8e41}

.button:active {
  background-color: #3e8e41;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}
</style>
