<template>
    <div class="todo-header">
          <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="add"/>
    </div>
</template>

<script>
    import {nanoid} from 'nanoid'
    export default {
        name: 'MyHeader',
        //props:['addTodo'], //改为自定义事件，不用props
        data() {
            return {
                title:''
            }
        },
        methods: {
            add(){
                //校验数据
                if(this.title.trim()){
                    //将用户的输入包装成一个todo对象
                    const todoObject = {id:nanoid(),title:this.title,done:false};
                    //通知App组件去添加一个todo对象
                    //this.addTodo(todoObject);
                    this.$emit('addTodo',todoObject);//改为自定义事件传递消息
                }else{
                    alert('输入不能为空！');
                }
                //添加完后input框置为空
                this.title = '';
            }
        },
    }
</script>

<style scoped>
  /*header*/
  .todo-header input {
    width: 560px;
    height: 28px;
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 4px 7px;
  }

  .todo-header input:focus {
    outline: none;
    border-color: rgba(82, 168, 236, 0.8);
    box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
  }
</style>