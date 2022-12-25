<template>
  <div class="wrapper">
     <h1>task menu</h1>
<div>
<form class="inputfield" @submit.prevent="create">
<input v-model="newtodo" autocomplete="off">
<button @click="create" >add task</button>

</form>

</div>
<ul class="todolist">
<li v-for="item in todos" :key="item.id" >
<H3 :class="{done: item.completed}" @click="completed(item)">{{ item.content }}</H3>
<button @click="remove(item)">delete task</button>
</li>

</ul>
<div class="footer">

<button @click="markall">select all</button>

</div>
</div>

</template>

<script>
import { ref } from 'vue'

export default{
  setup() {
const todos = ref([])
const newtodo =ref('')
function create(){
  todos.value.push({
    id:Date.now(),
    content:newtodo.value,
    completed: false

  })
  newtodo.value = ''
}


function remove(item) {

todos.value.splice(todos.value.indexOf(item),1)

}

function completed(item){
item.completed = !item.completed
}

function markall(){
todos.value.forEach((todo) => todo.completed=true)

}


    return{
      todos,
      newtodo,
      create,
      remove,
      completed,
      markall
    }

  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  font-family: 'poppins', sans-serif;
}
body{
  width:100%;
  height: 100vh;
  padding: 10px;
  background: #a9a9a9;
}
.wrapper{
  background:#fff;
  max-width: 400px;
  width: 100%;
  margin: 120px auto;
  padding: 25px;
  border-radius: 25px;
  box-shadow: 0px 10px 15px rgba(0,0,0,.1);
}
input{
  width: 97%;
  margin: 20px 0;
  height: 100%;
  border-radius:  3px;
  border: 1px solid #ccc;
  font-size: 17px;
  padding:15px 5px ;
  transition: all 0.3s ease;
}
form button{
  width: 100%;
  height: 100%;
  border: none;
  color: #fff;
  margin-left: 5px;
  font-size: 21px;
  outline: none;
  background: #454548;
  cursor: pointer;
  border-radius: 3px;
  pointer-events: none;
  transform: all 0.3s ease ;
}
.wrapper .todolist{
margin-top: 20px;
max-height: 250px;
overflow-y: auto;
}
li{
  position: relative;
  list-style:  none;
  margin-bottom: 8px;
  background: #d3d3d3;
  border-radius: 3px;
  padding: 10px 15px;
  cursor: default;
  overflow: hidden;
  word-wrap: break-word;
}
.footer{
  display: flex;
  width: 100%;
  margin-top: 20px;
  align-items: center;
  justify-content: space-between;
}
.footer button{
  padding: 6px 10px ;
  border-radius: 3px;
  border: none;
  color: #fff;
  background: #295538;
  cursor: pointer;
}
.done{
  text-decoration: line-through;
}
.item{
  cursor: pointer;
}

.done {
  text-decoration: line-through;
}
</style>
