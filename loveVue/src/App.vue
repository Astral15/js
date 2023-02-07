<script>
import ToDoList from './ToDoList.vue'
import ToDoitemForm from './ToDoitemForm.vue'
export default {
    components: {
        ToDoList ,
        ToDoitemForm
    },
    data() { 
      return {
        search: null,
        todos: [
          { id: 1, name: "to do item", done: false },
          { id: 2, name: "to do item 2", done: false },
          { id: 3, name: "to do item 3", done: false },
        ]
      }
    },
   methods: {
    putNewItemIntoTodoList(data){
      this.todos.push({
        id: this.nextId,
        name: data,
        done: false
      })
    },
    changeStatus(record){
      let v = this.todos.find(item=> item.id === record.id)
       v.done = !v.done
    },
    deleteItemFromTodoList(record){
      let v = this.todos.find(item => item.id === record.id)
      this.todos.splice(this.todos.indexOf(v), 1)
    }
   },
   computed: {
    nextId(){
      return this.todos.length + 1
    },
    activeTodos(){
      return this.todos.filter(value=> value.done === false)
    },
    doneTodos(){
      return this.todos.filter(value=> value.done === true)
    },
    filteredTodos(){
      return (this.search != null && this.search.length > 2) 
        ? this.todos.filter(value=> value.name.toLocaleLowerCase().includes(this.search.toLocaleLowerCase()))
        : this.todos
    }
   }
}
</script>

<template>
  <div class="container">
    <div class="todos">
      <ToDoitemForm @onSubmit="putNewItemIntoTodoList($event)"/>
      <h2>All Todo Items</h2>
      <ToDoList :data="todos"/>

      <h2>Active Todos</h2>
      <ToDoList :changeStatus="true" :data="activeTodos" @onChangeStatus="changeStatus($event)"/>

      <h2>ToDo With Done Status</h2>
      <ToDoList :canDelete="true" :data="doneTodos" @onDelete="deleteItemFromTodoList($event)" />
    </div>
    <div class="filter">
      <h2>Filter</h2>
      <input type="text" v-model="search"/>
      <ToDoList :data="filteredTodos"/>
    </div>
  </div>
</template>