<template>
  <p :class="['todo_item', item.completed?'is-completed':'']">
      <input type="checkbox" :checked="item.completed" @change="markItemComplated">
      {{item.title}}
      <button class="btn-del" @click="deleteItem">Delete</button>
  </p>
</template>

<script>
// import { ref } from "vue";
export default {
    name:'TodoItem',
    props:{
        item: {
            type: String,
            default: ''
        }
    },
    setup(props, context){
        const markItemComplated = () => {
            context.emit('item-completed',props.item.id)
        }
        const deleteItem = () => {
            context.emit('item-delete',props.item.id)
        }
        return{
            markItemComplated,
            deleteItem
        }
    }
}
</script>

<style scoped>
.todo_item{
    background-color: #f4f4f4;
    padding: 10px;
    margin: 0;
    border-bottom: 1px solid #ccc;
}
.btn-del{
    background-color: #ff0000;
    color: white;
    cursor: pointer;
    border: none;
    float: right;
}
.is-completed{
    text-decoration: line-through;
}
</style>