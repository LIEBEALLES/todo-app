<template>
  <div>
    <header>
      <h1>TODO-APP</h1>
    </header>
    <main>
      <TodoInput :item="todoText" @input="updateTodoText" @add="addTodoItem" />
      <TodoListItem v-for="(todoItem, index) in todoItems" :key="index" :todoItem="todoItem" :index="index" @remove="removeItem"/>
    </main>
  </div>
</template>


<script lang="ts">
import Vue from "vue";
import TodoInput from "./components/TodoInput.vue";
import TodoListItem from "@/components/TodoListItem.vue";

const STORAGE_KEY = 'vue-todo-ts-v1'
const storage = {
  save(todoItems : any[]){
    const parsed = JSON.stringify(todoItems)
    localStorage.setItem(STORAGE_KEY, parsed);
  },
  fetch(){
    const todoItems = localStorage.getItem(STORAGE_KEY) || [];
    const result = JSON.parse(todoItems);
    return result;
  },
}
export default Vue.extend({
  components: { TodoListItem, TodoInput },
  created() {
    this.fetchTodoItems();
  },
  methods: {
    init(){
      this.todoText = ""
    },
    updateTodoText(value: string) {
      this.todoText = value;
    },
    addTodoItem() {
      const value = this.todoText;
      this.todoItems.push(value);
      storage.save(this.todoItems)
      this.init();
    },
    fetchTodoItems(){
      this.todoItems = storage.fetch();
    },
    removeItem(index : number){
      this.todoItems.splice(index,1);
      storage.save(this.todoItems);
    }

  },
  data() {
    return {
      todoText: "",
      todoItems : []
    };
  }

});
</script>