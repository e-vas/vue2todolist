<template>
  <div id="todolist">

    <v-card class="mx-auto" max-width="500" >
        <img alt="Vue logo" src="https://cdn-icons-png.flaticon.com/512/6056/6056529.png" width="100">
        <h1>
          to do list
        </h1>

      <v-input>
        <v-text-field label="Add task" v-model="newTask" />
        <v-btn class="mx-2" fab dark small color=#69a563f0 v-on:click="inputGetValue">
          <v-icon dark>
            mdi-plus
          </v-icon>
        </v-btn>
      </v-input>

      <v-list>
        <TodoList v-for="todos in todos" :key="todos.id" v-bind:todos="todos" v-on:deleteTask="deleteTask"
          v-on:checBoxTask="checBoxTask" />
      </v-list>

    </v-card>



  </div>
</template>

<script>
import TodoList from '@/components/TodoItem';
export default {
  name: 'App',
  data() {
    return {
      todos: [],
      newTask: "",

    }
  },
  beforeCreate() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=10')
      .then(response => response.json())
      .then(json => {
        this.todos = json
        //console.log('create new item')
      })
  },
  methods: {
    rules() {

    },

    inputGetValue() {
      let uuid = Date.now();
      this.todos.push({ id: uuid, title: this.newTask, complited: false })
      this.newTask = " "

    },

    checBoxTask(id) {
      let index = this.todos.findIndex(item => item.id === id)
      if (this.todos[index].complited === true) {
        this.todos[index].complited = false
      } else {
        this.todos[index].complited = true
      }
      console.log(index)
      console.log(this.todos[index].complited)

    },
    deleteTask(id) {
      let index = this.todos.findIndex(item => item.id === id)
      //this.todos = this.todos.filter(item => item.id !== id)
      this.todos.splice(index, 1)
      //console.log(index)

    },

  },
  components: {
    TodoList
  }
}
</script>

<style>
#todolist {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #888f96;
  margin-top: 60px;

}

ul {
  list-style: none;
  text-align: left;
  margin-left: 480px;
  font-size: 20px;
}
</style>