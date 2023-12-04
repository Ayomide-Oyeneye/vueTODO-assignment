<template>
  <div class="container">
    <h1 class="hello">Todo App</h1>
    <hr>
    <div class="select-cont">
      <input type="text" id="todo-input" @keyup.enter="addTodoList" v-model="newTodo"
        placeholder="Enter your todo here" />
      <button @click="addTodoList"><img width="50" height="50" src="https://img.icons8.com/nolan/24/plus-math.png"
          alt="plus-math" /></button>
    </div>
    <ul>
      <li v-for="(todos, index) in todo" :key="index" class="todo-stl">
        <span v-if="!todos.edit">{{ todos.text }}</span>
        <input class="update" type="text" v-if="todos.edit" v-model="todos.text" @keyup.enter="saveEdit(todos)"
          @keyup.esc="cancellEdit(todos)">
        <div class="btn-div">
          <button class="edi btns" @click="editingTodo(todos)"><img width="20" height="20"
              src="https://img.icons8.com/material-outlined/24/edit--v1.png" alt="edit--v1" /></button>
          <button class="dele btns" @click="deleteTodo(index)"><img width="20" height="20"
              src="https://img.icons8.com/material-outlined/24/trash--v1.png" alt="trash--v1" /></button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: "",
      todo: [],
      editTodo: null,
    };
  },
  methods: {
    addTodoList() {
      if (this.newTodo.trim() != "") {
        this.todo.push({ text: this.newTodo, edit: false })
        this.newTodo = ''
      }
    },
    editingTodo(todos) {
      todos.edit = true;
      this.editTodo = todos
    },
    saveEdit(todos) {
      todos.edit = false;
      this.editTodo = null
    },
    cancellEdit(todos) {
      todos.edit = false
      this.editTodo = null
    },
    deleteTodo(index) {
      this.todo.splice(index, 1)
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
* {
  font-family: monospace;
  margin: 0;
  padding: 0;
}

body {
  background-image: linear-gradient(to top, rgb(46, 63, 63), #0e5ed6);
  height: 100vh;

}

.hello {
  font-size: 5rem;
  font-weight: 900;
  text-align: center;
}

.todo-stl {
  background-color: rgb(179, 177, 177);
  padding-inline-start: 10px;
  color: rgb(0, 0, 0);
  list-style: none;
  align-items: center;
  justify-content: space-between;
  font-size: 2.5rem;
  font-weight: bolder;
  margin-inline-start: 0;
  margin-block: 0.5rem;
  width: 100%;
  overflow-x: hidden;
}

ul {
  margin-inline: 0;
  padding: 0;
}

.container {
  display: flex;
  flex-direction: column;
  margin: 200px auto;
  border-radius: 0.5rem;
  background-color: rgb(255, 255, 255);
  max-width: 50%;

  padding-inline: 1rem;
  height: auto;
}

#todo-input {
  height: 4rem;
  background-color: transparent;
  outline: none;
  border: 1px solid grey;
  font-size: 2rem;
  width: 100%;
  margin-inline-end: 5px;
  border-radius: 0.2rem;
}

.update {
  height: 4rem;
  background-color: rgb(49, 49, 48);
  font-size: 2rem;
  outline: none;
  border: 1px solid grey;
  color: rgb(248, 227, 198);
  width: 50%;
  margin-inline: 5px;
  margin-block: 5px;
  border-radius: 0.2rem;
}

.select-cont button {
  height: 4rem;
  text-align: center;
  border-radius: 0.5rem;
  margin-inline-start: 1px;
  padding-inline: 0.5rem;
  border: none;
  background-image: linear-gradient(to top, rgb(119, 0, 255), rgb(0, 217, 255));
}

.select-cont {
  margin: 0 auto;
  align-items: center;
  display: flex;
  max-width: 100%;
  min-width: 50%;
  margin-top: 10px;
  margin-bottom: 10px;
}

#todo-input::placeholder {
  font-size: 2rem;
  font-weight: 800;
}

.btn-div .btns {
  margin-inline-start: 1rem;
  padding: 1rem;
  border-radius: 0.2rem;
}

.btn-div .dele {
  margin-inline-start: 0.5rem;
  background-color: red;
}

.btn-div .edi {
  background-color: rgb(69, 255, 69);
}
@media screen and (max-width: 499px) {
  .container {
  display: flex;
  flex-direction: column;
  margin: 200px auto;
  border-radius: 0.5rem;
  background-color: rgb(255, 255, 255);
  max-width: 90%;
  padding-inline: 1rem;
  height: auto;
}
}
</style>

