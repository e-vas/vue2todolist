<template>
  <div id="todolist">
    <v-app>
      <v-card class="mx-auto rounded-xl pb-3" width="500">
        <div class="d-flex justify-center flex-row align-center">
          <v-img alt="Vue logo" src="https://cdn-icons-png.flaticon.com/512/6056/6056529.png" max-height="70"
            max-width="70" contain></v-img>
          <h1>
            to do list
          </h1>
        </div>
        <div class="d-flex flex-rowa align-center rounded-lg me-3 ms-5" elevation="5">
          <v-text-field label="Add task" v-model="newTask" v-on:keyup.enter="inputGetValue" counter="50" />
          <v-btn class="mx-2" fab dark small color=#69a563f0 v-on:click="inputGetValue">
            <v-icon dark>
              mdi-plus
            </v-icon>
          </v-btn>
        </div>

        <v-list class="d-flex flex-column">
          <TodoList v-for="todos in todos.toReversed().slice(itemsStart, itemsEnd)" :key="todos.id" v-bind:todos="todos"
            v-on:deleteTask="deleteTask" v-on:checBoxTask="checBoxTask" />
        </v-list>

        <div class="text-center">
          <v-pagination v-model="page" :length="total" :total-visible="5" @input="changeTab"></v-pagination>
        </div>

      </v-card>


    </v-app>
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
      total: 0,
      page: 1,
      itemsStart: 0,
      itemsEnd: 10,

    }
  },
  beforeCreate() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=32')
      .then(response => response.json())
      .then(json => {
        this.todos = json
        //console.log('create new item')

      })

  },
  updated() {
    this.total = Math.ceil(this.todos.length / 10);

  },

  methods: {
    rules() {

    },

    inputGetValue() {
      if (this.newTask != "" && this.newTask != " " && this.newTask.length <= 50) {
        let uuid = Date.now();
        this.todos.push({ id: uuid, title: this.newTask, complited: false })
        this.newTask = ""
      }


    },

    checBoxTask(id) {
      let index = this.todos.findIndex(item => item.id === id)
      if (this.todos[index].complited === true) {
        this.todos[index].complited = false
      } else {
        this.todos[index].complited = true
      }
      //console.log(this.total)
      //console.log(this.todos[index].complited)

    },
    deleteTask(id) {
      let index = this.todos.findIndex(item => item.id === id)
      //this.todos = this.todos.filter(item => item.id !== id)
      this.todos.splice(index, 1)
      console.log(index)
      if (this.todos.length % 10 == 0) {
        this.page = this.total - 1
        this.changeTab()
        console.log("total if: " + this.total)
      }
      console.log("total: " + this.total)
      console.log(this.todos.length)


    },
    changeTab() {
      this.itemsEnd = (this.page * 10)
      this.itemsStart = this.itemsEnd - 10
    }

  },
  components: {
    TodoList,
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

h1 {
  color: #0000009a;
}
</style>