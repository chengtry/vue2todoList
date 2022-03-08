<template>
    <div>
        <li>
            <label>
                <input type="checkbox" :checked="todoObject.done" @click="handleCheck(todoObject.id)"/>
                <span v-show="!todoObject.isEdit">{{todoObject.title}}</span>
                <input
                type="text" 
                v-show="todoObject.isEdit"  
                :value="todoObject.title"
                @blur="handleBlur(todoObject,$event)"
                ref="inputTitle"
                />
            </label>
            <button class="btn btn-danger" @click="handleDelete(todoObject.id)">删除</button>
            <button v-show="!todoObject.isEdit" class="btn btn-edit" @click="handleEdit(todoObject)">编辑</button>
        </li>
    </div>
</template>

<script>
    export default {
        name: 'MyItem',
        //props:['todoObject',"checkTodo","deleteTodo"],
        props:['todoObject'],
        methods: {
            //勾选或者取消勾选
            handleCheck(id){
                //通知App组件并将对应的todo对象的done值取反
                //this.checkTodo(id);
                this.$bus.$emit('checkTodo',id); //改为全局事件总线进行组件之间通信
            },
            //删除指定id的todo对象
            handleDelete(id){
                //this.deleteTodo(id);
                this.$bus.$emit('deleteTodo',id); //改为全局事件总线进行组件之间通信
            },
            //编辑
            handleEdit(todoObject){
              if(Object.prototype.hasOwnProperty.call(todoObject,'isEdit')){
                todoObject.isEdit = true;
              }else{
                this.$set(todoObject,'isEdit',true);
              }
              this.$nextTick(function(){
                this.$refs.inputTitle.focus();
              })
            },
            //失去焦点回调（真正执行修改逻辑）
            handleBlur(todoObject,e){
              todoObject.isEdit = false;
              if(!e.target.value.trim()) return alert('输入不能为空！')
              this.$bus.$emit('updateTodo',todoObject.id,e.target.value)
            }
        },
    }
</script>

<style scoped>
  /*item*/
  li {
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
  }

  li label {
    float: left;
    cursor: pointer;
  }

  li label li input {
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
  }

  li button {
    float: right;
    display: none;
    margin-top: 3px;
  }

  li:before {
    content: initial;
  }

  li:last-child {
    border-bottom: none;
  }
  li:hover{
      background-color: #ddd;
  }
  li:hover button{
      display: block;
  }
</style>