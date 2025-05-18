<!-- Dalten Hansen-White and Ezekiel Torres-->
<script setup>
import { useTodoListStore } from '../stores/todoList'
import { storeToRefs } from 'pinia'
import { ref } from 'vue'

const store = useTodoListStore()
const { toggleCompleted, deleteTodo } = store
const { todoList, incomplete } = storeToRefs(store) //added incomplete getter
const filter = ref(false)

</script>

<template>
    <button @click="filter = !filter">Filter</button>
    <div v-if="filter == false" class="filter">All Tasks</div>
    <div v-else class="filter">Incomplete Tasks</div>           <!-- setup filter button and display-->
    <div v-if="filter == false">
    <div v-for="todo in todoList" :key="todo.id" class="item">
        <div class="content">
            <span :class="{ completed: todo.completed }">{{ todo.item }}</span>
            <span @click.stop="toggleCompleted(todo.id)">&#10004;</span>
            <span @click="deleteTodo(todo.id)" class="x">&#10060;</span>
            </div>
        </div>
    </div>
    <div v-else>
     <div v-for="todo in incomplete" :key="todo.id" class="item">   <!-- added filter list for completed todos-->
        <div class="content">
            <span :class="{ completed: todo.completed }">{{ todo.item }}</span>
            <span @click.stop="toggleCompleted(todo.id)">&#10004;</span>
            <span @click="deleteTodo(todo.id)" class="x">&#10060;</span>
            </div>
        </div>
     </div>
     
</template>

<style scoped>
span {
    margin: 0 10px;
    cursor: pointer;
}
.item {
    display: flex;
    justify-content: center;
}
.content {
    display: flex;
    font-size: 1.5em;
    justify-content: space-between;
    width: 80vm;
    padding: 5px;
}
.completed {
    text-decoration: line-through;
}
button {
    margin-left: 10px;
    background-color: #2f6089;
    padding: 5px 10px;
    border: none;
    border-radius: 5px;
    font-weight: 800;
    color: white;
    width: 20%;
}
</style>