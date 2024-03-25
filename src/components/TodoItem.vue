<script setup>
import CheckIcon from  '@/components/Icons/CheckIcon.vue'
import TrashCan from  '@/components/Icons/TrashCan.vue'
import PencilIcon from  '@/components/Icons/PencilIcon.vue'

  const props = defineProps({
    todo: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    }
  })

  defineEmits(['toggle-complete', 'edit-todo', 'update-todo', 'delete-todo'])

</script>

<template>
  <li class="flex bg-zinc-200 px-4 py-2 justify-between rounded-md items-center group shadow-lg">
    <div class="flex gap-2">
      <input type="checkbox"  @input="$emit('toggleComplete', index)" :checked="todo.isCompleted" class="appearance-none size-5 bg-white rounded-full shadow checked:bg-green-600/80 cursor-pointer"/>
      <input type="text" class="border border-green-600 px-2  outline-none focus-within:border-blue-500 rounded-md" :value="todo.todo" v-if="todo.isEditing" @input="$emit('update-todo', $event.target.value, index)"/>
      <span v-else :class="{'line-through tracking-wide': todo.isCompleted}">{{ todo.todo }}</span>
    </div>
    <div class="flex gap-2 ml-2 opacity-0 group-hover:opacity-100 transition-all">
      <CheckIcon
        v-if="todo.isEditing" 
        class="size-7 text-green-500 cursor-pointer"
        @click="$emit('edit-todo', index)"
      />
      <PencilIcon 
        v-else 
        class="size-7 text-blue-400 cursor-pointer"
        @click="$emit('edit-todo', index)"
      />
      <TrashCan 
        class="size-7 text-red-500 cursor-pointer"
        @click="$emit('delete-todo', todo.id)"
      />
    </div>
  </li>
</template>