<template>
  <div id="app" class="container">
    <h1 class="text-center">Todo App</h1>
    <input
      v-model="todoText"
      type="text" 
      class="w-100 p-2" 
      placeholder="Type Todo"
      @keyup.enter = "addTodo" 
    >
    <!-- v-model를 통해 이벤트가 끝나면 빈값을 보여줌. keyUP은 키보드 이벤트-->
    <hr>
    <div class="w-100">
      <span >입력한 글자:</span>
      {{todoText}}
      </div>
    <hr>
    <Todo 
      v-for="todo in todos" 
      :key="todo.id"
      :todo = "todo"
      @toggle-checkbox="toggleCheckbox"
      @click-delete ="deleteTodo"
      />
  </div>
</template>

<script>
import Todo from '@/components/Todo.vue'; //다른 vue파일 임포트

export default {
  components: { //컴포넌트 등록
    Todo
  },
  data() {
    return{
      todoText: '',
      todos: [
        { 
          id: 1,
          text: 'buy a car',
          checked: false
        },
        { 
          id: 2, 
          text: 'play a game', 
          checked: false
        },
      ] //todos 배열
    }
  },
  methods: {
    deleteTodo(id){
      // const index= this.todos.findIndex(todo => {
      //   return todo.id === id;
      // });
      // this.todos.splice(index,1); //배열 삭제
      this.todos = this.todos.filter(todo => todo.id !==id); // 해당 id번호가 아닌것들만 필터링 해서 보여줌.
    },

    addTodo(e) {
      this.todos.push({
        id: Math.random(), //정확한 키 값이 없어서 랜덤 값을 키값 설정
        text:e.target.value, //배열에 넣을때 인풋 value값을 넣음.
        checked: false //기본 체크 값은 false임. 할 일을 다 했을때 밑줄 긋기위해 체크를 만듬.
        });
        this.todoText=""; //위 이벤트가 끝나면 input value값은 빈값을 보여주게 함.
    },
    toggleCheckbox({id, checked}){
      const index = this.todos.findIndex(todo => {
        return todo.id === id; //위에 있는 todo배열에서 todo.id와 체크한 id의 값을 찾아줌.
      });
      this.todos[index].checked = checked;
    }
  }
}
</script>
