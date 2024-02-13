<template>
  <div>
  <h4>To do</h4>
  
  <div class="filter-div">
    <select v-model="todoFilter" class="filter-drop">
      <option>all</option>
      <option>type1</option>
      <option>type2</option>
      <option>completed</option>
    </select>
  </div>
  <div class="todos">
    <todo-item 
      v-for="todo in filterTodos"
      :key="todo._id"
      :todoProp="{
        name: todo.name,
        isCompleted: todo.isCompleted,
        type: todo.type
      }"  
      @complSwap="completedHandler(todo._id)" 
      @remove="removetodo(todo._id)"
    >
    </todo-item>
  </div>
  
  <div class="add-todo">
    <input type="text" placeholder="todo name" v-model="todoName"/>

    <select v-model="todoType" class="type-drop">
      <option>type1</option>
      <option>type2</option>
    </select>
    
    <button @click="addtodo()">+</button>
  </div>
  </div>
</template>

<script>
import todoItem from './components/todoItem.vue'

export default {
  name: 'App',
  data(){
    return {
      todoName: "",
      todoType: "type1",
      todoFilter: "all",
      todos: []
    };
  },
  methods: {
    completedHandler: function (todoId) {
      const  currenttodo = this.todos.find((t) => t._id === todoId);
      currenttodo.isCompleted = !currenttodo.isCompleted;
    },
    addtodo: function () {
      this.todos.push(
        {
          _id: Math.random().toString(36).substring(4, 9),
          name: this.todoName,
          isCompleted: false,
          type: this.todoType
        }
      );
    },
    removetodo: function (todoId) {
      this.todos = this.todos.filter((t) => t._id !== todoId);
    }
  },
  computed: {
    filterTodos() {
      return this.todos.filter((t) => {
        return this.todoFilter == "all" ||
          this.todoFilter == "type1" && t.type == "type1" && t.isCompleted == false ||
          this.todoFilter == "type2" && t.type == "type2" && t.isCompleted == false ||
          this.todoFilter == "completed" && t.isCompleted == true;
      });
    }
  },
  components: {
    todoItem
  }
}
</script>

