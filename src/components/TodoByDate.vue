<template>
  <div class="plate" v-if="todos.length > 0">
    <h4 style="font-family: 'Days One'; cursor: default; color: #7E7E7E;">{{todos[0].date}}</h4>
    <transition-group name="user-list">
      <TodoListItem
        v-for="todo in todos"
        :key="todo"
        :content="todo.content" 
        :id="todo.id" 
        :progress="todo.inProgress" 
        :date="todo.date" 
      />
    </transition-group>
  </div>

</template>

<script>
import TodoListItem from "@/components/TodoListItem.vue";
export default {
  components: {TodoListItem},
  props: {
    todos: {
      type: Array,
      required: true,
    }
  },
  
}
</script>

<style scoped>
  
</style>

    