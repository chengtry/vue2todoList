<template>
    <div class="todo-footer" v-show="total>0">
        <label>
        <input type="checkbox" :checked="isAll" @change="checkAll"/>
        </label>
        <span>
        <span>已完成{{doneTotal}}</span> / 全部{{total}}
        </span>
        <button class="btn btn-danger" @click="clear">清除已完成任务</button>
    </div>
</template>

<script>
    export default {
        name: 'MyFooter',
        props:['todos','checkAllTodo','clearTodo'],
        computed:{
            total(){
                return this.todos.length;
            },
            doneTotal(){
                //普通写法
                /*let i = 0;
                this.todos.filter((todo)=>{
                    if(todo.done) i++;
                })
                return i;*/
                //高级写法reduce
                return this.todos.reduce((pre,todo)=>{
                    return pre + (todo.done ? 1 : 0);
                },0)
            },
            isAll(){
                return this.doneTotal === this.total && this.total > 0;
            }
        },
        methods: {
            //全选或者取消全选
            checkAll(e){
                //console.log(e.target.checked)
                this.checkAllTodo(e.target.checked);
            },
            //清除已完成任务
            clear(){
                this.clearTodo();
            }
        },
    }
</script>

<style scoped>
  /*footer*/
  .todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
  }

  .todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
  }

  .todo-footer label input {
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
  }

  .todo-footer button {
    float: right;
    margin-top: 5px;
  }
</style>