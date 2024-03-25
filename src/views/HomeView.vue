<script setup>
import TodoForm from '@/components/TodoForm.vue';
import TodoItem from '@/components/TodoItem.vue';
import SadIcon from '@/components/Icons/SadIcon.vue'
import PartyPopper from '@/components/Icons/PartyPopper.vue'
import { ref, watch, computed } from 'vue';
import { uid } from 'uid'

const todoList = ref([]);

watch(todoList, () => {
  setTodoLocalStorate()
}, {deep: true})

const todoCompleted = computed(() => {
  return todoList.value.every((todo) => todo.isCompleted)
})

const fetchTodoList = () => {
  const savedTodoList = JSON.parse(localStorage.getItem('todoList'))
  if(savedTodoList){
    todoList.value = savedTodoList
  }
}

fetchTodoList()

const setTodoLocalStorate = () => {
  localStorage.setItem('todoList', JSON.stringify(todoList.value))
}

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null
  })
}

const toggleTodoComplete = (todoPos) => {
  todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted
}

const toggleEditTodo = (todoPos) => {
  todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing
}

const updateTodo = (todoVal, todoPos) => {
  todoList.value[todoPos].todo = todoVal;
}

const deleteTodo = (todoId) => {
  todoList.value = todoList.value.filter((todo) => todo.id !== todoId)
}

</script>

<template>
  <main class="flex items-center w-full min-h-screen flex-col pt-10">
    <div class="flex gap-2 flex-col">
      <h2 class="text-center font-sans font-bold text-xl">Create todo</h2>
      <TodoForm  @create-todo="createTodo"/>
      <p v-if="todoCompleted && todoList.length > 0" class="flex gap-2 justify-center items-center mt-3"> <PartyPopper class="size-7"/> You have completed all your todos!</p>
      <ul class="mt-8 flex flex-col gap-4" v-if="todoList.length > 0">
        <TodoItem  
          v-for="(todo, index) in todoList" 
          :todo="todo" 
          :index="index" 
          @toggle-complete="toggleTodoComplete"
          @edit-todo="toggleEditTodo"
          @update-todo="updateTodo"
          @delete-todo="deleteTodo"
        />
      </ul>
      <p v-else class="flex mt-6 gap-2 items-center justify-center text-xl">
        <SadIcon class="size-10" /> 
        No todos created...
      </p>
    </div>
  </main>
</template>
