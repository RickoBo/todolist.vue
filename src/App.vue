<template>
  <div id="app">
    <div class="todo">
      <input @keyup.enter="handleTodoInput" v-model="todoInputValue" placeholder="type your shit here"
             class="todo__input">
      <ul class="todo__list">
        <li v-for="(todo, index) in todosArray" :key="todo" class="todo_item">
          <input v-on:click="handleCheckboxClick(index)" type="checkbox" v-model="todo.checked">

          <span v-if="todo.editable === false" :class="todo.checked ? 'text__linethrough' : ''">
            {{ todo.text }}
          </span>
          <input @keyup.enter="handleEditClick(index)" v-else type="text" v-model="todo.text"
                 @input="(e) => todo.text = e.target.value">
          <button @click="handleEditClick(index)">{{ todo.editable ? "Submit" : "Edit" }}</button>
          <button @click="handeleDeleteClick(index)">Delete</button>
        </li>
        <!--        <li class="todo_item">-->
        <!--          <input type="checkbox">-->
        <!--          <span class="text__linethrough">Покормить собаку</span>-->
        <!--          <button>edit</button>-->
        <!--          <button>delete</button>-->
        <!--        </li>-->
      </ul>
    </div>

  </div>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    todoInputValue: '',
    todosArray: [
      {
        editable: false,
        checked: true,
        text: "Покормить собаку",
      },
      {
        editable: false,
        checked: false,
        text: "Написать todolist",
      }
    ]
  }),

  methods: {
    handleCheckboxClick(index) {
      this.todosArray[index].checked = !this.todosArray[index].checked
    },
    handleTodoInput(e) {
      if (e.target.value === '') {
        return
      }
      // text from the input - e.target.value
      this.todosArray.push({
        checked: false,
        text: e.target.value,
      })
      this.todoInputValue = ''
    },
    handeleDeleteClick(index) {
      this.todosArray.splice(index, 1)
    },
    handleEditClick(index) {
      this.todosArray[index].editable = !this.todosArray[index].editable
    }
  },
}

</script>

<style>

/*#app {*/
/*  font-family: Avenir, Helvetica, Arial, sans-serif;*/
/*  -webkit-font-smoothing: antialiased;*/
/*  -moz-osx-font-smoothing: grayscale;*/
/*  text-align: center;*/
/*  color: #2c3e50;*/
/*  margin-top: 60px;*/
/*}*/
.todo {
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin: 0 auto;
  width: 300px;
}

.todo__input {

}

.todo__list {
  padding: 0;
}

.todo_item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  list-style-type: none;
  margin-bottom: 10px;

}

.text__linethrough {
  text-decoration: line-through;
}

</style>
