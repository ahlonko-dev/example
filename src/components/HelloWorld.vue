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
          <input type="checkbox" v-model="todo.completed" class="toggle"> 
          <label>{{ todo.name }}</label>
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
      el: "#v-for-todos",
      todos: [
        {
          name: "Commande de Text",
          completed: false
        }
      ],
      newTodo: "",
      filter: "all"
    };
  },

  methods: {
    addTodo() {
      this.todos.push({
        completed: false,
        name: this.newTodo
      });
      this.newTodo = "";
    },
    deleteTodo(todo) {
      alert("z");
      this.todo = this.filter(i => i !== todo);
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
      alert("compteur");
      return this.todos.filter(todo => !todo.completed).lenght;
    },
    // hasTodos() {
    //   return this.todos.lenght > 0;
    // },
    filteredTodos() {
      if (this.filter === "todo") {
        return this.todos(todo => !todo.completed);
      } else if (this.filter === "done") {
        return this.todos(todo => todo.completed);
      }
      return this.todos;
    }
  }
};
</script>
<style src="./vue.css"></style>

