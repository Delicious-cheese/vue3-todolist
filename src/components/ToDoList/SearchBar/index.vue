<template>
    <div class="search-container">
        <input type="text" placeholder="输入待办事项" v-model="inpTxt">
        <div class="search-btn">
            <button @click="getToDoItem">添加</button>
            <button @click="searchTodoItem">搜索</button>
            <button @click="clearItem">清空搜索</button>
            <button @click="freshItem">查看所有</button>
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const inpTxt = ref('')
const emit = defineEmits(['newTodoContent', 'searchTodo', 'freshList'])

const getToDoItem = () => {
    emit('newTodoContent', inpTxt.value)
}

const searchTodoItem = () => {
    emit('searchTodo', inpTxt.value)
}

const clearItem = () => {
    inpTxt.value = ''
}

const freshItem = () => {
    emit('freshList')
}

</script>

<style>
.search-container {
    width: 100%;
    display: flex;
    justify-content: space-between;
}

.search-container input {
    width: 40%;
    height: 25px;
}

.search-container .search-btn {
    width: 56%;
    display: flex;
    justify-content: flex-end;
}

button {
    margin: 0 6px;
    height: 36px;
}
</style>