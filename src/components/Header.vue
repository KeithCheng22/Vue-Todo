<template>
    <section class="flex">
    <h1 class="font-Clash font-bold text-2xl p-5">What's up, <input class='outline-none bg-transparent text-blue-900' autocomplete="off" placeholder="Enter Name" type="text" name='name' v-model="name" /></h1>
    </section>
</template>

<script setup>
    import { ref, onMounted, watch } from 'vue';
    const name = ref('')

    watch(name, (newVal) => {
        localStorage.setItem('name', newVal)
    })

    onMounted(() => {
        if (!localStorage.getItem('name')) {
            localStorage.setItem('name', name.value)
            return
        }
        name.value = localStorage.getItem('name')
    })
</script>