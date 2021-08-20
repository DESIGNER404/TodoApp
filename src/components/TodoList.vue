<template>
  <div class="container">
    <h1>{{ title }}</h1>
    <pre>{{ notes }}</pre>
    <form v-on:submit.prevent="hruchevo">
      <input v-model="message" placeholder="Итем" />
      <input v-model="price" placeholder="цена" />
      <input v-model="kol" placeholder="Количество" />
      <button ref="add_btn" v-bind:disabled="isDisabled">
        Добавить элемент
      </button>
    </form>
    <button @click="clearList" v-bind:disabled="isDisabledTwo">Очистить</button>
    <hr />
    <h3 v-show="notes.length === 0">Ничего нет</h3>
    <ul>
      <li v-for="note in notes" :key="note.id">
        {{ note.name }} <button @click="priceDec(note)">&laquo;</button>
        {{ note.count }} <button @click="priceInc(note)">&raquo;</button> за
        единицу: <input v-model="note.price" type="" /> цена:
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
    {{ ArraySort }}
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
      price: 0,
      kol: 1,
    };
  },

  computed: {
    ArraySort() {
      let itog = 0;
      for (let i = 0; i < this.notes.length; i++) {
        let item = this.notes[i];
        let sum = item.price * item.count;
        itog = sum + itog;
        console.log(sum);
      }
      return itog;
    },

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
      // let hue = parseInt(Math.random() * 256);
      // this.$refs.add_btn.style.background = `hsl(${hue},70% ,30%)`;
      this.notes.push({
        name: this.message,
        count: this.kol,
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
  color: white;
  margin-left: auto;
  margin-right: auto;
  background-color: rgba(59, 59, 59, 0.979);
  max-width: 600px;
  border: 3px solid rgb(252, 172, 1);
  border-radius: 10px;
  padding: 10px;
  box-shadow: 0px 0px 20px rgba(255, 217, 1, 0.5);
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
