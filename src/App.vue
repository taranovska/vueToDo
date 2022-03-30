<template>
  <div id="app">
    <AddTodo @add-todo="addTodo" />
    <div class="flexbox">
      <Board id="board-1" class="board1">
        <TodoList v-bind:todos="todos" @remove-todo="removeTodo" />
      </Board>
      <div>
        <div class="todoByDay">
          <p>{{ currentDate }}</p>
          <p>Total:</p>
          <p>Done:</p>
        </div>

        <Board id="board-2"> </Board>
        <div class="todoByDay">
          <p>{{ nextDate }}</p>
          <p>Total:</p>
          <p>Done:</p>
        </div>

        <Board id="board-3"> </Board>
      </div>
    </div>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
import AddTodo from "@/components/AddTodo";
import Board from "./components/Board";

export default {
  name: "app",
  components: { TodoList, AddTodo, Board },
  data() {
    return {
      todos: [],
      todaysTodos: [],
      tomorrowsTodos: [],
      currentDate:
        String(new Date().getDate()).padStart(2, "0") +
        "." +
        String(new Date().getMonth() + 1).padStart(2, "0"),
      nextDate:
        String(
          new Date(new Date().getTime() + 24 * 60 * 60 * 1000).getDate()
        ).padStart(2, "0") +
        "." +
        String(
          new Date(new Date().getTime() + 24 * 60 * 60 * 1000).getMonth() + 1
        ).padStart(2, "0"),
    };
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter((t) => t.id !== id);
    },
    addTodo(todo) {
      this.todos.push(todo);
      todo.sort((a, b) => {
        return new Date(a.time) - new Date(b.time);
      });
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  background-color: #f3f3f3;
}
.flexbox {
  display: flex;
  justify-content: center;
  min-height: 200px;
  margin: 0 auto;
  padding: 15px;
}
.flexbox .board {
  display: flex;
  flex-direction: column;
  min-width: 300px;
  background-color: white;
  padding: 15px;
  min-height: 300px;
  border-radius: 20px;
}
.flexbox .board .card {
  padding: 15px 25px;

  cursor: pointer;
  margin-bottom: 15px;
}
.board {
  min-height: 200px;
  -webkit-box-shadow: 4px 4px 8px 10px rgba(34, 60, 80, 0.26);
  -moz-box-shadow: 4px 4px 8px 10px rgba(34, 60, 80, 0.26);
  box-shadow: 4px 4px 8px 10px rgba(34, 60, 80, 0.26);
}
#board-1 {
  background-color: #efefef;
  margin-right: 100px;
}
.todoByDay {
  display: flex;
  justify-content: space-around;
  margin-bottom: 10px;
}
</style>
