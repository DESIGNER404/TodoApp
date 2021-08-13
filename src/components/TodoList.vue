<template>
  <div class="container">
    <h1>{{ title }}</h1>
    <form v-on:submit.prevent="hruchevo">
      <input v-model="message" />
      <button ref="add_btn" v-bind:disabled="isDisabled">
        Добавить хрючево
      </button>
    </form>
    <button @click="clearList" v-bind:disabled="isDisabledTwo">Очистить</button>
    <pre>[{{ message }}]</pre>
    <pre>[{{ message.trim() }}]</pre>
    <hr />
    <ul>
      <li v-for="(note, index) in notes" :key="note">
        {{ note }} {{ vl }}
        <button
          @click="deleteElement(index)"
          style="
            border-radius: 100%;
            padding: 0px;
            margin-top: 10px;
            width: 25px;
            height: 25px;
          "
        >
          х
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  data() {
    return {
      title: "Список хруючева",
      message: "",
      notes: [],
      vl: "",
    };
  },

  computed: {
    isDisabled() {
      if (this.message != "") {
        return false;
      } else {
        return true;
      }
    },
    isDisabledTwo() {
      if (this.notes != "") {
        return false;
      } else {
        return true;
      }
    },
  },

  methods: {
    hruchevo() {
      this.$refs.add_btn.style.background = "red";
      this.notes.push(this.message);
      this.clear();
    },
    clear() {
      this.message = "";
    },
    clearList() {
      this.notes = [];
    },
    deleteElement(position) {
      this.notes.splice(position, 1);
    },
  },
};
</script>

<style scoped lang="scss">
.container {
  margin-left: auto;
  margin-right: auto;
  background-color: rgba(92, 161, 245, 0.666);
  max-width: 400px;
  border: 1px solid gray;
  border-radius: 10px;
  padding: 10px;
  box-shadow: 0px 0px 10px rgba(24, 24, 24, 0.475);
  & hr {
    border: 1px solid rgb(226, 166, 15);
  }
  & input {
    padding: 8px;
    border-radius: 3px;
  }
  & button {
    cursor: pointer;
    padding: 10px;
    margin-left: 10px;
    background-color: rgb(226, 166, 15);
    border-radius: 3px;
    border: 0px;
    box-shadow: 0px 0px 10px rgba(255, 162, 0, 0.769);
    &:hover {
      background-color: rgb(189, 115, 24);
    }
  }
}
</style>
