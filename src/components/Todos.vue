<template>
    <AddTodo @add-todo="addTodo"/>
    <TodoItem 
    v-for="todo in todos" 
    :key="todo.id" 
    :item="todo"
    @item-completed="markCompleted"
    @item-delete="deleteItem"
    
    />
</template>

<script>
import { ref } from "vue";
import AddTodo from "./AddTodo";
import TodoItem from "./TodoItem";
import axios from "axios";
export default {
    name:'Todos',
    components:{
        TodoItem,
        AddTodo
    },
    setup(){
        const todos = ref([])

        const getAllTodos = async () =>{
            try {
                const res = await axios.get(
                    'https://jsonplaceholder.typicode.com/todos?_limit=5'
                    )
               todos.value = res.data
            } catch (error) {
                console.log(error)
            }
        }
        getAllTodos()
        const markCompleted = id => {
            todos.value.map(todo =>{
                if(todo.id === id) todo.completed = !todo.completed
                return todo
            })
        }

        const deleteItem = async id => {
            try {
                await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
                todos.value = todos.value.filter(todo => todo.id !== id)
            } catch (error) {
                console.log(error)
            }
        }
        const addTodo = async newTodo =>{
            try {
                const res = await axios.post(`https://jsonplaceholder.typicode.com/todos`,newTodo)
                todos.value.push(res.data)
            } catch (error) {
                console.log(error)
            }
            
        }
        return{
            deleteItem,
            todos,
            markCompleted,
            addTodo

        }
    }
}
</script>

<style>

</style>