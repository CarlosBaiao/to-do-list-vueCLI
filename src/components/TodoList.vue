<template>
  <div class="todo-list">
    <div class="container">
      <input
        type="text"
        class="input-new-item"
        v-model="toDo"
        v-on:keyup.enter="addNewItemToListbyKeyboard"
        placeholder="Digite sua Tarefa"
      />
      <button @click="addNewItemToListbyBotton">adicionar</button>
    </div>

    <ul>
      <ListItem
        v-for="(item, index) in list"
        :key="index"
        :item="item"
        :index="index"
        @delete-item="deleteItem"
      />
    </ul>

    <button class="removeAll" @click="removeAllList" :disabled='!isDisabled'>Apagar todas Tarefas</button>
  </div>
</template>

<script>
import ListItem from "./ListItem.vue";

export default {
  name: "TodoList",
  components: {
    ListItem,
  },
  data() {
    return {
      list: [],
      toDo: "",
    };
  },
  created() {
    const itensInLocalStorage = JSON.parse(localStorage.getItem("list"));
    this.list = itensInLocalStorage ? itensInLocalStorage : [];
  },
  computed: {
    isDisabled () {
      return this.list.length > 0;
    }
  },
  methods: {
    addNewItemToListbyBotton() {
      if (this.toDo.length == 0) return;
      this.list.unshift({
        label: this.toDo,
        checked: false,
      });
      this.toDo = "";
    },
    addNewItemToListbyKeyboard(event) {
      let newItem = event.target.value;
      if (newItem.length == 0) return;
      this.list.unshift({
        label: newItem,
        checked: false,
      });
      this.updateLocalStorage();
      event.target.value = " ";
      
    },
    removeAllList() {
      this.list.splice(0, this.list.length)
    },
    deleteItem(index) {
      this.list.splice(index, 1);
    },
    updateLocalStorage() {
      localStorage.setItem("list", JSON.stringify(this.list));
    },
  },
  watch: {
    list() {
      this.updateLocalStorage();
    },
  },
};
</script>

<style scoped lang="less">
.todo-list {
  width: 600px;
  margin: 30px auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  background: @bg-grey;
  padding: 50px;
  border-radius: 5px;


  
.container {
  display: flex;
  justify-content: space-between;
  width: 100%;
  

  .input-new-item {
    width: 75%;
    outline: none;
    height: 40px;
    padding: 0 30px;
    border: none;
    border-radius: 5px;
    font-size: 16px;
  

    &::placeholder {
      text-align: center;
      font-size: 15px;

    }
  }

  button {
      border: none;
      background: @orange;
      color: white;
    }
}

ul {
  list-style: none;
  padding: 0;
  width:90%;
  margin: 20px auto;

}

.removeAll {
  background: white;
  color: @orange;
  width: 40%;

  &:disabled {
    color: @bg-grey;
    cursor:no-drop;
  }
}

@media @tablets {
  width: 400px;
  padding: 20px;

  .container {
    flex-direction: column;
    align-items: center;


    .input-new-item {
      width: 100%;
    }
  }

  button {
    width: 60%;
    margin-top: 20px;
  }

  .removeAll {
    width: 60%;
  }
}

@media @smartphones {
  width: 300px;
}

}
</style>
