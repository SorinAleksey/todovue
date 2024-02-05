<template>
  <div 
      class="todo" 
      :class="{completed: isCompleted}"
      @click="$emit('complSwap')"
    >
      <div class="round" :class="classtodoType()"></div>
      
      <span>{{name}}</span>

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
  props: ['_id', 'name', 'isCompleted', 'type'],
  emits: ['remove', 'complSwap'],
  methods: {
    classtodoType: function () {
      return {
        type1: this.type === 'type1', 
        type2: this.type === 'type2'
      }
    }
  }
}
</script>

