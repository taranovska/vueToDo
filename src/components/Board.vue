<template>
  <div :id="id" class="board" @dragover.prevent @drop.prevent="drop">
    <slot />
  </div>
</template>

<script>
export default {
  props: ["id"],
  methods: {
    drop: (e) => {
      const todo_id = e.dataTransfer.getData("todo_id");
      const todo = document.getElementById(todo_id);
      todo.style.display = "block";
      e.target.appendChild(todo);
    },
  },
};
</script>
<style>
.board {
  padding: 15px 25px;
  background-color: red;
  cursor: pointer;
  margin-bottom: 15px;
}
</style>
