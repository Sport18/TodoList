<template>
    <div class='todo-footer'>
        <label>
            <input 
            type="checkbox" 
            v-model="isCheck"
            />
        </label>
        <span>
            <span>已完成{{finishedCount}}件</span> / 总计{{todos.length}}件
        </span>
        <button 
            class="btn btn-warning" @click="delFinishedTodos"
        >清除已完成任务</button>
    </div>
</template>

<script>
export default {
    name: 'Footer',
    props:{
        todos:Array,
        selectedAllTodo:Function,
        delFinishedTodos:Function,
    },
    data() {
        return {
        
        }
    },
    computed:{
        finishedCount(){
            return this.todos.reduce((total,todo) => total + (todo.finished ? 1 : 0),0 )
        },
        isCheck:{
            get(){
                return this.finishedCount === this.todos.length && this.todos.length > 0;
            },
            set(value){
                this.selectedAllTodo(value);
            },
        }
    }
}
</script>

<style scoped>
    .todo-footer label {
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
    }

    .todo-footer button {
        float: right;
        margin-top: 5px;
    }
</style>
