<template>
    <div class="todo-container">
        <div class="todo-wrap">
            <Header
                :addTodo="addTodo"
            ></Header>
            <List 
                :todos="todos" 
                :delTodo="delTode"
            ></List>
            <Footer
                :todos="todos"
                :selectedAllTodo="selectedAllTodo"
                :delFinishedTodos="delFinishedTodos"
            ></Footer>        
        </div>
    </div>
</template>

<script>
    // 引入组件
    import Header from './components/Header'
    import List from './components/List'
    import Footer from './components/Footer'

    // 引入工具类
    import localStorageUtil from './utils/localStorageUtil'

    export default {
        name: 'app',
        data(){
            return {
                todos:localStorageUtil.readTodos()
            }
        },
        components: {
            Header,
            List,
            Footer,
        },
        methods:{
            //根据索引删除一条记录
            delTode(index){
                this.todos.splice(index,1)
            },
            // 添加一条数据
            addTodo(todo){
                this.todos.unshift(todo);
            },
            // 是否选中所有任务
            selectedAllTodo(isCheck){
                this.todos.forEach(todo => {
                    todo.finished = isCheck
                })
            },
            // 删除已选的任务
            delFinishedTodos(){
                if(window.confirm("您确定要清除所有已完成任务吗？")){
                    this.todos = this.todos.filter(todo => !todo.finished)
                }
            }
        },
        watch: {
            // 深度监视
            todos:{
                deep:true,
                immediate:true,
                handler:localStorageUtil.saveTodos,
            }
        }
    }
</script>

<style scoped>
    .todo-container {
        width: 600px;
        margin: 0 auto;
    }

    .todo-container .todo-wrap {
        padding: 10px;
        border: 1px solid #ddd;
        border-radius: 5px; /*向 div 元素添加圆角边框： */
    }
</style>>