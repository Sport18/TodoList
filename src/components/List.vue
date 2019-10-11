<template>
	<ul class="todo-main">
        <Item
            v-for="(todo,index) in todos"
            :todo="todo"
            :index="index"
            :delTodo="delTodo"
        ></Item>
    </ul>
</template>

<script>
    import Item from './Item'
    export default {
        name: 'List',
        props:{
            todos:Array,
            delTodo:Function,
        },
        
        components: {
            Item,
        },
        methods: {}
    }
</script>

<style scoped>
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
	padding-left: 5px;
	margin-top: 10px;
}
</style>
