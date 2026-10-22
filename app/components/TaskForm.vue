<template>
    <div>
        <form @submit.prevent="handleSubmit()" class="flex flex-col p-3 w-max gap-3">
            <h2 class="font-semibold text-xl">Nouvelle Tâche</h2>
            <div class="flex   w-max gap-3">
            <input v-model="title" id="title" class=" outline-none text-gray-700 text-xs p-2 border border-gray-400/40 rounded-sm bg-white " type="text" placeholder="Titre de la tache...">
             
            <select v-model="category"   name="category" id="category" class=" outline-none  text-xs w-50  px-2 border border-gray-400/40 rounded-sm bg-white ">
                <option value="Personnel">Personnel</option>
                <option value="Travail">Travail</option>
                <option value="Urgent">Urgent</option>
            </select>
            <button :disabled="disabledButton()" type="submit" class="btn btn-primary ">Ajouter</button>
            </div>
        </form>
    </div>
</template>

<script setup lang="ts">
import type { Task } from '~/types/task'

const title = ref<string>('')
const category = ref<string>('')

const emit = defineEmits<{ 'add-task': [task: Pick<Task, 'title' | 'category'>] }>()
function disabledButton(){
    if(!(title.value.trim() &&category.value) )
    return true
}
function handleSubmit(){
    emit('add-task', { title: title.value.trim() , category: category.value})
    title.value=''
    category.value=''
}

</script>