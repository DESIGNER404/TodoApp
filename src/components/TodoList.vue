<template>
  <div class="container">
    <h1>{{ title }}</h1>
    <!-- <pre>{{ notes }}</pre> -->
    <form v-on:submit.prevent="hruchevo">
      <input v-model="message" />
      <input v-model="price" />
      <button ref="add_btn" v-bind:disabled="isDisabled">
        Добавить элемент
      </button>
    </form>
    <button @click="clearList" v-bind:disabled="isDisabledTwo">Очистить</button>
    <hr />
    <h3 v-show="notes.length === 0">Тут нихуя нет</h3>
    <ul>
      <li v-for="note in notes" :key="note">
        {{ note.name }} <button @click="priceDec(note)">&laquo;</button>
        {{ note.count }} <button @click="priceInc(note)">&raquo;</button> цена:
        {{ note.price * note.count }}
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
    {{}}
  </div>
</template>

<script>
export default {
  name: "TodoList",
  data() {
    return {
      title: "Добавить элемент",
      message: "",
      notes: [],
      nextTodoId: 1,
      price: 10,
    };
  },

  computed: {
    isDisabled() {
      if (this.message.trim() != "") {
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
      //let color = Math.floor(Math.random()*(999999 - 111111 + 1)) + 111111;
      // this.$refs.add_btn.style.background = `#${color}`;
      let hue = parseInt(Math.random() * 256);
      this.$refs.add_btn.style.background = `hsl(${hue},70% ,30%)`;
      this.notes.push({
        name: this.message,
        count: 1,
        id: this.nextTodoId,
        price: this.price,
      });
      this.clear();
      this.nextTodoId++;
    },
    clear() {
      this.message = "";
      this.price = "";
    },
    clearList() {
      this.notes = [];
    },
    deleteElement(position) {
      this.notes.splice(position, 1);
    },
    priceDec(item) {
      item.count--;
      if (item.count < 1) {
        item.count = 1;
      }
    },
    priceInc(item) {
      item.count++;
    },
  },
};
</script>

<style scoped lang="scss">
.container {
  margin-left: auto;
  margin-right: auto;
  background-color: rgba(92, 161, 245, 0.666);
  max-width: 450px;
  border: 1px solid gray;
  border-radius: 10px;
  padding: 10px;
  box-shadow: 0px 0px 10px rgba(24, 24, 24, 0.475);
  & h1 {
    color: white;
  }
  & form {
    display: inline-block;
  }
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
