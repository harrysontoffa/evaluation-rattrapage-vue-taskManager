<template>
   <div class="flex items-center gap-3 bg-base-100 rounded-box shadow-sm px-4 py-3">
        <input @change="handleChecked()" type="checkbox" :checked="props.task.isComplete"  class="checkbox   checkbox-primary  " />
        <p class="font-medium " :class="{ 'line-through text-gray-400': props.task.isComplete }">{{ props.task.title }}</p>
        <p class="badge badge-outline">{{ props.task.category }}</p>
        <button @click="handleDelete()" class="btn btn-error btn-sm ml-auto">Supprimer</button>
    </div>
</template>

<script setup lang="ts">
import type { Task } from '~/types/task';

const props = defineProps<{task:Task}>()

const emit = defineEmits<{
  'toggle-complete': [id: Task['id']]
  'delete-task': [id: Task['id']]
}>()

function handleChecked(){
    emit('toggle-complete', props.task.id)
}

function handleDelete(){
    emit('delete-task',   props.task.id)
}



</script>