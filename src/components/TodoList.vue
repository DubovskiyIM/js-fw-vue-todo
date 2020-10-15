<template>
  <div class="container">
    Add Todo:
    <label>
      <input type="text" v-model="title">
    </label>
    <button @click="addTodo">Add Todo</button>
    <hr>
    Todos:
    <ul>
      <TodoItem v-for="(todo, idx) of todos.list"
                :key="idx"
                :todo="todo"
                :idx="idx"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from '@/components/TodoItem';
export default {
  name: 'TodoList',
  components: {
    TodoItem
  },
  data() {
    return {
      title: '',
      todos: []
    }
  },
  async created() {
    let data = await fetch('https://kodaktor.ru/j/tasklist').then(x => x.json());
    this.todos = await data;
  },
  methods: {
    addTodo() {
      if (this.title.trim()) {
        const newTodo = this.title
        this.todos.list.push(newTodo)
        this.title = '';
      }
    }
  }
};
</script>

<style scoped>
ul {
  list-style-type: none;
  font-size: 24px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
button {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  height: 40px;
  padding: 10px;
  margin: 10px;
  background-color: lightblue;
  border: none;
  outline: none;
  border-radius: 5px;
  cursor: pointer;
  opacity: 1;
  transition: opacity .4s;
}
button:hover {
  opacity: .8;
}
input {
  outline: none;
  border: 2px solid grey;
  border-radius: 3px;
  padding: 10px;
  transition: border .4s;
}
input:focus {
  border: 2px solid lightblue;
}
.container {
  text-align: left;
}
</style>
