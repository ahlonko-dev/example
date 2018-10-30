<template>
  <section class="todoapp">
    <header class="header">
      <h1>Commandes</h1>
      <input type="text" class="new-todo" placeholder="Ajouter une Commande" v-model="newTodo" @keyup.enter="addTodo">

    </header>
    <div class="main">
      <input class="toggle-all" type="checkbox"  v-model="allDone">
      <ul class="todo-list" id="">
        <li class="todo" v-for="todo in filteredTodos" :class="{ completed: todo.completed }" :key="todo.id">
          <div class="view">
          <input type="checkbox" v-model="todo.completed"  @click='completeTodo' class="toggle"> 
          <label>{{ todo.id }} {{ todo.name }}</label>
            <button class="destroy" @click.prevent="deleteTodo(todo)"></button>
            </div>
        </li> 
      </ul>
    </div>
    
    <footer class="footer" >  
      <!-- v-show="hasTodos" -->
      <span class="todo-count"><strong>{{ remaining }}</strong> Commande (s) </span>
      <ul class="filters">
        <li><a href="#" :class="{selected: filter === 'all'}" @click.prevent="filter= 'all'">Toues commandes</a> </li>
        <li><a href="#" :class="{selected: filter === 'todo'}" @click.prevent="filter= 'todo'">à faire</a> </li>
        <li><a href="#" :class="{selected: filter === 'done'}" @click.prevent="filter= 'done'">faites</a> </li>
        </ul>
      </footer>
  </section>
</template>

<script>
export default {
  data() {
    return {
      currentTodoId: 1,
      el: "",
      todos: [
        {
          id: 0,
          name: "Tâche test",
          femme: "",
          homme: "",
          date: "",

          completed: false
        }
      ],
      newTodo: "",
      newDate: "",
      filter: "all"
    };
  },

  methods: {
    completeTodo() {},
    addTodo() {
      this.todos.push({
        id: this.currentTodoId++,
        completed: false,
        name: this.newTodo
      });
      this.newTodo = "";
    },
    deleteTodo(todo) {
      this.todos = this.todos.filter(i => i !== todo);
    }
  },
  computed: {
    allDone: {
      get() {
        return this.remaining === 0;
      },
      set(value) {
        this.todos.forEach(todo => {
          todo.completed = value;
        });
      }
    },
    remaining() {
      return this.todos.filter(todo => !todo.completed).length;
    },
    // // hasTodos() {
    //   return this.todos.lenght > 0;
    // // },
    filteredTodos() {
      if (this.filter === "todo") {
        return this.todos.filter(todo => !todo.completed);
      } else if (this.filter === "done") {
        return this.todos.filter(todo => todo.completed);
      }
      return this.todos;
    }
  }
};
</script>
<style src="./vue.css"></style>

