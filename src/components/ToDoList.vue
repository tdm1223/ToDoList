<template>
<div class="container">
  <div class="page-header" style="background:skyblue">
    <h1 class="text-center">TO DO LIST</h1>
  </div>
  <div class="input-group" style="margin-bottom:10px;">
    <input type="text" class="form-control" placeholder="할일을 입력하세요" v-model="name" v-on:keyup.enter="createTodo(name)">
    <span class="input-group-btn">
      <button class="btn btn-default" type="button" @click="createTodo(name)">추가</button>
    </span>
  </div>
  <div class="row">
    <div class="col-xs-12">
      <ul class="list-group">
        <li class="list-group-item" v-for="(todo, index) in todos"> 
            <template v-if="todo.icon"><span class="glyphicon glyphicon-star" @click="important(index)"></span></template>
            <template v-else><span class="glyphicon glyphicon-star-empty" @click="important(index)"></span></template>
            <span> {{todo.name}}</span>
          <div class="btn-group pull-right" style="font-size: 12px; line-height: 1;">
            <button type="button" class="btn-link dropdown-toggle" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
              더보기<span class="caret"></span>
            </button>
            <ul class="dropdown-menu">
              <li><a href="#" @click="deleteTodo(index)">삭제</a></li>
            </ul>
          </div>
        </li>
      </ul>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'ToDoList',
  data () {
    return {
      todos: [
        {
          name:'청소',
          icon:true
        },
        {
          name:'블로그 쓰기',
          icon:false
        },
        {
          name:'밥먹기',
          icon:false
        },
      ]
    }
  },
  methods:{
    deleteTodo(i){
      this.todos.splice(i,1);
    },
    createTodo(name){
			if(name != null){
				this.todos.push({name:name,icon:false});
				this.name = null
			}
		},
    important(i){
      if(this.todos[i].icon==true){
        this.todos[i].icon=false;
      }else{
        this.todos[i].icon=true;
      }
    }
  }
}
</script>