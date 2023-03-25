<template>
    <div class="container">
        <SearchBar @newTodoContent="(value) => addTodo(value)" @searchTodo="(value) => searchTodo(value)"
            @freshList="() => freshItems()" />
        <ToDoItem v-for="item in curListData" :key="item.id" :item="item" @delete="(value) => deleteTodo(value)"
            @change="(value) => changeToDo(value)" />
    </div>
</template>

<script setup lang="ts">
import SearchBar from './SearchBar/index.vue'
import ToDoItem from './ToDoItem/index.vue'
import { ref } from 'vue'


const listData = ref([
    { content: 'vue', id: crypto.randomUUID(), done: false },
    { content: 'react', id: crypto.randomUUID(), done: false },
    { content: 'angular', id: crypto.randomUUID(), done: true },
    { content: 'lalallalllllllllllllllllllllllllllllll海岸hiahiahi哎嗨嗨啊安徽ID哎嗨嗨啊安徽ID哎嗨嗨啊安徽IDhiOA阿富汗酸辣粉拿水立方', id: crypto.randomUUID(), done: false },
])



const curListData = ref()
curListData.value = [...listData.value]


const addTodo = (content) => {
    const todo = listData.value.find(item => item.content === content)
    if (todo) {
        alert('任务重复了，请重新输入')
        return;
    }

    if (content) {
        listData.value.push({ content, id: crypto.randomUUID(), done: false })
        curListData.value = [...listData.value]
    } else {
        alert('代办事项不能为空')
    }

}

const searchTodo = (content) => {
    curListData.value = [...listData.value.filter(item => item.content == content)]
}

const deleteTodo = (id) => {
    listData.value = listData.value.filter(item => item.id !== id)
    curListData.value = [...listData.value]
}

const freshItems = () => {
    curListData.value = [...listData.value]
}

const changeToDo = (id) => {
    const index = listData.value.findIndex(item => item.id === id)
    let tmp = listData.value.find(item => item.id === id)
    if (tmp) {
        tmp = {
            ...tmp,
            done: !tmp.done
        }
        listData.value.splice(index, 1, tmp)
        curListData.value = [...listData.value]

    }

}
</script>

<style>
.container {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    width: 660px;
}
</style>