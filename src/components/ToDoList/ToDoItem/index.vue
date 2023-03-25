<template>
    <div class="content-container">
        <div class="left">
            <input type="checkbox" :checked="props.item.done" @click="changgeD">
            <span :class='props.item.done ? "text" : ""'>{{ props?.item?.content }}</span>
        </div>
        <button @click="deleteItem">删除</button>
    </div>
</template>

<script setup lang="ts">

const props = defineProps(['item'])
const emit = defineEmits(['delete', 'change'])

const deleteItem = () => {
    emit('delete', props.item.id)
}

const changgeD = () => {
    emit('change', props.item.id)
}
</script>

<style>
.content-container {
    width: 100%;
    /* overflow: hidden; */
    display: flex;
    justify-content: space-between;
    margin-top: 10px;
}

.content-container .left {
    width: 70%;
    text-align: left;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}

.content-container .left input {
    vertical-align: middle;
}

.content-container button {
    width: 10%;
}

.text {
    text-decoration: line-through;
}
</style>