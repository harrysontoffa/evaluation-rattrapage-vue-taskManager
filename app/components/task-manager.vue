<template>
 <div class="flex flex-col gap-3 bg-gray-500/20  p-4 w-max"> 
        <TaskForm @add-task="handleAddTask"  ></TaskForm>
        <template v-if="taches.length>0"> 
          <TaskItem  @toggle-complete="handleToggleComplete" @delete-task="handleDeletask"  v-for="tache in taches" :key="tache.id" :task=tache ></TaskItem>
        </template>
        <p v-else>Aucune tâche</p>

 </div>
</template>

<script setup lang="ts">
 
import type { Task } from '~/types/task';

const taches = ref<Task[]>([
    {id: '1',title: 'Acheter du café ', category:'Personnel', isComplete: false},
    {id: '2',title: 'Préparer le cours vue 3', category:'Travail', isComplete: false}
])
function handleAddTask(event: { title: string; category: string }){
     

  taches.value.push({ id: crypto.randomUUID(), ...event, isComplete: false })

}
function handleDeletask(event:string){

   taches.value =  taches.value.filter(tache => tache.id !== event)
}

function handleToggleComplete(event: string){
    const tache = taches.value.find(tache => tache.id === event)
    if(tache) tache.isComplete = !tache.isComplete

}

</script>