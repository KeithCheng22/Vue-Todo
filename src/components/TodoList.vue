<template>
    <section class="p-5">
        <h3 class="font-Clash">Todo List</h3>

        <div v-show="todoList.length === 0">
            <small>Empty...</small>
        </div>

       <div v-for="todoItem in todoList" :key='todoItem.id' class="border bg-white p-2 rounded-md shadow-sm mt-1 flex justify-between" :class="todoItem.category === 'business' ? 'border-blue-900' : 'border-red-900'">
            <div class="flex items-center gap-1 w-full">
                <input type="checkbox" class='cursor-pointer' :class="todoItem.category === 'business' ? 'border border-blue-900 before:bg-blue-900' : ' border border-red-900 before:bg-red-900'" @click="updateTodoStatus(todoItem.id)" :style="todoItem.completed ? {transform:'scale(0.8)'} : ''" :checked='todoItem.completed'/>

                <input type="text" class="outline-none font-Clash w-[95%] text-wrap" :class="todoItem.completed ? 'line-through text-slate-500' : ''" v-model='todoItem.todo' @change="editedTodo()"/>
            </div>

            <button class="bg-red-500 text-white px-[0.4rem] rounded-sm hover:bg-red-800 transition-background duration-150" @click="deleteTodo(todoItem.id)">X</button>
       </div>
    </section>
</template>

<script setup>
    const props = defineProps({
        todoList: {
            type: Array,
            required: true
        }
    })

    const emit = defineEmits([
        'update-todo-status',
        'delete-todo',
        'edit-todo'
    ])

    const updateTodoStatus = (id) => {
        emit('update-todo-status', id)
    }

    const deleteTodo = (id) => {
        emit('delete-todo', id)
    }

    const editedTodo = () => {
        emit('edit-todo')
    }
</script>