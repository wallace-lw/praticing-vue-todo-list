<script setup>
import { reactive, ref } from 'vue';
import TodoButton from '@/components/TodoButton.vue'

  const emit = defineEmits(["create-todo"])

  const todoState = reactive({
    todo: "",
    invalid: null,
    errMsg: ""
  });
  
  const createTodo = () => {
    todoState.invalid = null;
    if(todoState.todo !== "") {
      emit("create-todo", todoState.todo)
      todoState.todo = "";
      return
    }
    todoState.invalid = true;
    todoState.errMsg = "Todo value cannot be empty.";
  }

</script>

<template>
  <div 
    class="border border-green-600 w-full sm:w-96 flex" 
    :class="{'border-red-500' : todoState.invalid}"
    >
    <input 
      type="text" 
      class="outline-none rounded-s-sm px-2 py-1 h-10 w-full" 
      v-model="todoState.todo" 
    />
    <TodoButton @click="createTodo()" />
  </div>
  <p class="text-red-500" v-show="todoState.invalid">{{ todoState.errMsg }}</p>
</template>
