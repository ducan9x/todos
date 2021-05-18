<template>
<p class="check" v-if="check">Nhập dữ liệu để thêm công việc</p>
  <form @submit="addItem">
        <input type="text" placeholder="Việc làm mới..." v-model="title">
        <input type="submit" value="Thêm" class="add-btn" />
  </form>
</template>

<script>
import {ref} from "vue";
export default {
    name:'AddTodo',
    setup(props,context){
        const title = ref('')
        const check = ref(false)
        const addItem = () =>{
                if(title.value.length > 0){

                    event.preventDefault()

                    const newItem = {
                       
                        title: title.value,
                        completed:false
                    }

                    context.emit('add-todo',newItem)

                    title.value = ''
                }
                else
                {
                    check.value = true
                }
                
            
        }
        return{
            title,
            addItem,
            check
        }
    }
}
</script>

<style scoped>
form{
    display: flex;

}
input[type = 'text']{
    flex: 10;
    padding: 5px;
}
input[type = 'submit']{
    flex: 2;
}
.check{
    color: red;
}
</style>