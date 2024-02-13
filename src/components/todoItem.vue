<template>
  <div 
      class="todo" 
      :class="{completed: todoProp.isCompleted}"
      @click="$emit('complSwap')"
    >
      <div class="round" :class="classtodoType"></div>
      
      <span>{{todoProp.name}}</span>

      <div class="remove" @click="$emit('remove')">
        <div class="round2">
          x
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'todo-item',
  props: {
    todoProp: Object
  },
  emits: ['remove', 'complSwap'],
  computed: {
    classtodoType() {
      return {
        type1: this.todoProp.type === 'type1', 
        type2: this.todoProp.type === 'type2'
      }
    }
  }
}
</script>

