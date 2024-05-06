<template>
    <section class="p-5 font-Clash">
        <h2>CREATE A TODO</h2>
        <h3>What's on your todo list?</h3>
        <form @submit.prevent="addNewTodo">
            <input class='shadow-sm rounded-md w-full p-2 mt-3 indent-2 outline-none' placeholder="e.g make a video" v-model="todo"/>

            <h3 class="mt-4">Pick a category</h3>
            <section class="flex justify-between mt-3 gap-3">

                <div class="flex flex-col bg-white w-[50%] p-5 gap-1 rounded-md shadow-sm items-center">
                    <input class='accent-blue-900' id='business' type="radio" name="category" v-model="category" value="business"/>
                    <label class="text-center" for="business">Business</label>
                </div>

                <div class="flex flex-col w-[50%] bg-white p-5 gap-1 rounded-md shadow-sm items-center">
                    <input class='accent-pink-900' id='personal' type="radio" name="category" v-model="category" value="personal"/>
                    <label class="text-center" for="personal">Personal</label>
                </div>
            </section>

            <button type="submit" class="w-full mt-4 bg-pink-500 p-2 rounded-md shadow-sm text-white hover:bg-pink-800 transition-backgroundColor duration-200">Add Todo</button>
        </form>
    </section>
</template>

<script setup>
    import { ref } from 'vue';
    const emit = defineEmits([
        'add-new-todo'
    ]);

    const category = ref(null);
    const todo = ref('');

    const addNewTodo = () => {
        const newTodo = {
            todo: todo.value, 
            category: category.value
        }
        emit('add-new-todo', newTodo)

        todo.value = '',
        category.value = null
    }

</script>