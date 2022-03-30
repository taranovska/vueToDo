<template>
  <Card id="{todo.id}" draggable="true" class="card">
    <div class="wrapper">
      <input type="checkbox" v-on:change="todo.completed = !todo.completed" />
      <li class="todoItem">
        <div class="todoFlex">
          <div>
            <div v-bind:class="{ done: todo.completed }">
              {{ String(new Date(todo.time).getHours()).padStart(2, "0") }}:{{
                String(new Date(todo.time).getMinutes()).padStart(2, "0")
              }}
            </div>
            <div v-bind:class="{ done: todo.completed }">
              {{ todo.title }}
            </div>
          </div>
          <div class="dots">
            &#8285; &#8285;
          </div>
        </div>
      </li>
      <button class="rm" v-on:click="$emit('remove-todo', todo.id)">
        &times;
      </button>
    </div>
  </Card>
</template>

<script>
import Card from "@/components/Card";
export default {
  props: {
    todo: {
      type: Object,
      required: true,
      dlTime:
        String(new Date().getHours()).padStart(2, "0") +
        ":" +
        String(new Date().getMinutes()).padStart(2, "0"),
    },
  },
  components: { Card },
};
</script>

<style scoped>
li {
  display: flex;
  justify-content: space-between;
  padding: 1rem 0.5rem;
}
.rm {
  background: rgba(112, 112, 112, 255);
  color: #fff;
  border: none;
  width: 20px;
  min-height: 20px;
  border-radius: 50%;
  font-weight: bold;
}
.todoItem {
  color: rgba(163, 171, 174, 255);
  border-radius: 10px;
  background-color: #d4eefa;
  padding: 15px;
  display: flex;
  margin-right: 10px;
}

.done {
  text-decoration: line-through;
}
.wrapper {
  display: flex;
  align-items: center;
}
.todoFlex {
  display: flex;
  width: 200px;
  justify-content: space-between;
  text-align: left;
}
.dots {
  font-size: 26px;
}
.wrapper input {
  margin-right: 10px;
}
</style>
