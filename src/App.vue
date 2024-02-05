<template>
  <div>
  <h4>To do</h4>
  <div class="todos">
    <todo-item 
      v-for="todo in todos" 
      :key="todo._id"
      :_id="todo._id" 
      :name="todo.name" 
      :isCompleted="todo.isCompleted" 
      :type="todo.type" 
      @complSwap="completedHandler(todo._id)" 
      @remove="removetodo(todo._id)"
    >
    </todo-item>
  </div>

  <div class="add-todo">
    <input type="text" placeholder="todo name" v-model="todoName"/>

    <select v-model="todoType" class="drop">
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
  components: {
    todoItem
  }
}
</script>

