<template>
  <div
    :id="id"
    class="card"
    :draggable="draggable"
    @dragstart="dragStart"
    @dragover.stop
  >
    <slot />
  </div>
</template>

<script>
export default {
  props: ["id", "draggable"],
  methods: {
    dragStart: (e) => {
      const target = e.target;
      e.dataTransfer.setData("todo_id", target.id);
      setTimeout(() => {
        target.style.display = "none";
      }, 0);
    },
  },
};
</script>

<style>
.flexbox .board .card {
  padding: 15px 25px;

  cursor: pointer;
  margin-bottom: 15px;
}
</style>
