<template>
    <div>
        <ul class="todo-main">
            <!-- <MyItem 
                v-for="todoObject in todos" 
                :key="todoObject.id" 
                :todoObject="todoObject" 
                :checkTodo="checkTodo"
                :deleteTodo="deleteTodo">
            </MyItem> -->
            <MyItem 
                v-for="todoObject in todos" 
                :key="todoObject.id" 
                :todoObject="todoObject" >
            </MyItem>
        </ul>
    </div>
</template>

<script>
    import MyItem from './MyItem'
    export default {
        name: 'MyList',
        components:{
            MyItem,
        },
        //props:['todos',"checkTodo","deleteTodo"]
        props:['todos'] //改为全局事件总线进行组件之间通信
    }
</script>

<style scoped>
  /*main*/
  .todo-main {
    margin-left: 0px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding: 0px;
  }

  .todo-empty {
    height: 40px;
    line-height: 40px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding-left: 5px;
    margin-top: 10px;
  }
</style>