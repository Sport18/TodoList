<template>
    <div class='Item'>
        <li
            @mouseenter="dealShow(true)"
            @mouseleave="dealShow(false)"
            :style="{backgroundColor:bgColor}"
        >
            <label>
                <input type="checkbox" v-model="todo.finished">
                <span>{{todo.title}}</span>
            </label>
            <button 
                class="btn btn-warning" v-show="isShowDelButton"
                @click="delItem"
            >删除</button>
        </li>
    </div>
</template>

<script>
    export default {
        name: 'Item',
        props:{
            todo:Object,
            index:Number, //当前任务在总任务数组中的下标位置
            delTodo:Function,
        },
        data(){
            return{
                isShowDelButton: false, //flase 隐藏 true 显示
                bgColor:'#fff',
            }
        },
        methods:{
            dealShow(isShow){
                //控制删除按钮的显示和隐藏
                //当鼠标加入当前li标签，删除显按钮示，离开后隐藏
                this.isShowDelButton = isShow;
                // 控制背景颜色
                this.bgColor = isShow ? '#ddd' : '#fff';
            },
            delItem(){
                if(window.confirm(`您确定删除 ${this.todo.title} 吗？`)){
                    this.delTodo(this.index)
                }
            }
        }
    }
</script>

<style scoped>
    li {
        list-style: none;
        height: 36px;
        line-height: 36px;
        padding: 0 5px;
        border-bottom: 1px solid #ddd;
    }

    li label {
        float: left;
        cursor: pointer; /* 该属性定义了鼠标指针放在一个元素边界范围内时所用的光标形状 */
    
    }

    li label li input {
        vertical-align: middle; /* 	该属性定义行内元素的基线相对于该元素所在行的基线的垂直对齐.把此元素放置在父元素的中部。 */
        margin-right: 6px;
        padding: relative;
        top: -1px;
    }

   li button{
       float: right;
       margin-top: 3px;
       padding: 5px 10px;
   } 

   li:before {
       content: initial;
   }

   li:last-child {
       border-bottom: none;
   }
</style>
