<template>
  <form @submit.prevent="onSubmit" class="formWrapper">
    <input
      type="text"
      placeholder="To-do..."
      v-model="title"
      class="wrapperElem"
    />
    <timeselector
      :displayFormat="'HH:mm'"
      :returnFormat="'HH:mm'"
      :interval="{ h: 1, m: 5 }"
      v-model="time"
      :placeholder="'DL'"
      :required="true"
      :displaySeconds="false"
      class="wrapperElem timeSel"
    ></timeselector>
    <button
      v-bind:class="{ add: !clicked, click: clicked }"
      v-on:click="clicked = !clicked"
      type="submit"
    >
      &#43;
    </button>
  </form>
</template>

<script>
import Timeselector from "vue-timeselector";
export default {
  data() {
    return {
      title: "",
      time: new Date(),
      clicked: false,
    };
  },
  methods: {
    onSubmit(e) {
      if (this.title.trim() && this.time) {
        const newTodo = {
          id: Date.now(),
          title: this.title,
          time: this.time,
          completed: false,
        };
        this.$emit("add-todo", newTodo);
        this.title = "";
      }
    },
  },
  components: {
    Timeselector,
  },
};
</script>

<style scoped>
.add {
  background: rgba(65, 194, 252, 255);
  border: none;
  color: #fff;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  font-weight: bold;
}
.click {
  background: rgba(65, 194, 252, 255);
  opacity: 0.5;
  border: none;
  color: #fff;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  font-weight: bold;
}
.formWrapper {
  display: flex;
  margin-right: 10px;
  justify-content: center;
  flex-wrap: wrap;
  margin-bottom: 20px;
}
.wrapperElem {
  margin-right: 20px;
}
input,
.timeSel {
  -webkit-box-shadow: 0px -2px 11px 2px rgba(34, 60, 80, 0.26);
  -moz-box-shadow: 0px -2px 11px 2px rgba(34, 60, 80, 0.26);
  box-shadow: 0px -2px 11px 2px rgba(34, 60, 80, 0.26);
  border: none;
}
</style>
