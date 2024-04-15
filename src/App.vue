<template>    
  <div class="h-[100vh] w-[80%] mx-auto max-w-[1000px] p-6">
    <Header />
    <TodoForm @add-new-todo="addTodo"/>
    <TodoList :todoList="todoList" @update-todo-status="updateTodoStatus" @delete-todo="deleteTodo" @edit-todo="editTodo"/>
  </div>
</template>


<script setup>
  // Component Imports
  import Header from './components/Header.vue';
  import TodoForm from './components/TodoForm.vue';
  import TodoList from './components/TodoList.vue';

  // Vue Imports
  import { ref, onMounted, watch } from 'vue';

  // Utils
  import { randomNumGenerator } from './utils'
  import { useToast } from "vue-toastification";
  
  const todoList = ref([])
  const toast = useToast()

  watch(todoList, (newVal) => {
    localStorage.setItem('todoList', JSON.stringify(newVal))
  }, {
    deep: true,
  })

  onMounted(() => {
    if (!localStorage.getItem('todoList')) {
            localStorage.setItem('todoList', JSON.stringify(todoList.value))
            return
        }
    todoList.value = JSON.parse(localStorage.getItem('todoList'))
    })

  // Add New Todo
  const addTodo = (newTodo) => {
    const { todo, category } = newTodo
    if (!todo || !category) {
      toast.error('Both fields must be filled!', {timeout: 3000})
      return
    }
    const newAddedTodo = {
      id: randomNumGenerator(),
      todo,
      category,
      completed: false
    }
      todoList.value.unshift(newAddedTodo)
      toast.success('Added Todo!', {timeout: 3000})
  }

  // Update Completion Status of Todo
  const updateTodoStatus = (id) => {
    const updatedTodo = todoList.value.find(todo => todo.id === id)
    updatedTodo.completed = !updatedTodo.completed
    if (updatedTodo.completed) {
      toast.success('Todo Done!', {timeout: 3000})
    }
  }

  const editTodo = () => {
    toast.success('Todo Edited!', {timeout: 3000})
  }

  //Delete Todo
  const deleteTodo = (id) => {
    todoList.value = todoList.value.filter(todo => todo.id !== id)
    toast.success('Todo Deleted!'), {timeout: 3000}
  }

</script>

