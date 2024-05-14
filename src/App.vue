<template>
  <div id="app">
    <h1>Tugas 3 Prak PBK CRUD</h1>
    <form @submit.prevent="addItem">
      <input v-model="newItem" placeholder="Add a new item" />
      <button type="submit" class="btn add">Add</button>
    </form>
    <ul>
      <li v-for="(item, index) in items" :key="index">
        <span v-if="!item.editing">{{ item.text }}</span>
        <input
          v-else
          v-model="item.text"
          @blur="updateItem(index)"
          @keyup.enter="updateItem(index)"
        />
        <button @click="editItem(index)" class="btn edit">
          {{ item.editing ? "Save" : "Edit" }}
        </button>
        <button @click="deleteItem(index)" class="btn delete">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newItem: "",
      items: [],
    };
  },
  methods: {
    addItem() {
      if (this.newItem.trim() !== "") {
        this.items.push({ text: this.newItem, editing: false });
        this.newItem = "";
      }
    },
    editItem(index) {
      this.items[index].editing = !this.items[index].editing;
    },
    updateItem(index) {
      if (this.items[index].text.trim() === "") {
        this.deleteItem(index);
      } else {
        this.items[index].editing = false;
      }
    },
    deleteItem(index) {
      this.items.splice(index, 1);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
  background-color: rgba(255, 255, 255, 0.7);
  border-radius: 20px;
}

form {
  margin-bottom: 20px;
  padding: 20px;
  margin: 20px;
}

input {
  padding: 5px;
  font-size: 16px;
}

button {
  margin-left: 10px;
  padding: 5px 10px;
  font-size: 16px;
  cursor: pointer;
  border: none;
  border-radius: 4px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

li span,
li input {
  flex-grow: 1;
}

li input {
  margin-right: 10px;
}

.btn.add {
  background-color: #4caf50;
  color: white;
}

.btn.edit {
  background-color: #2196f3;
  color: white;
}

.btn.delete {
  background-color: #f44336;
  color: white;
}
</style>
