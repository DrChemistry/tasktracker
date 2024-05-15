<template>
    <div>
        <h1>Tasks</h1>
        <p>Here are your tasks:</p>
        <ul>
            <li v-for="task in tasks" :key="task.id">
                {{ task.title }}
                <p>{{ task.description }}</p>
                <p>Interval: {{ task.interval }} days</p>
                <p>Due: {{ calculateDueDate(task).toLocaleString() }}</p>
                <p>Started: {{ task.startDate.toLocaleString() }}</p>
                <button @click="finishTask(task)">Finish Task</button>
                <!-- Progress bar to show when the task is due -->
                <progress :max="task.interval" :value="(currentDate - task.startDate) / (1000 * 60 * 60 * 24)"></progress>
            </li>
        </ul>
    </div>
</template> 

<script setup>
import { ref } from 'vue';


/*
   Every task has an id, title, description, and interval.
   The interval is the number of days between each time the task is due.
   It resets when the user chooses it.
*/

const currentDate = new Date();
const startDate1 = new Date();
startDate1.setDate(currentDate.getDate() - 1);
const startDate2 = new Date();
startDate2.setDate(currentDate.getDate() - 2);
const startDate3 = new Date();
startDate3.setDate(currentDate.getDate() - 3);
const startDate4 = new Date();
startDate4.setDate(currentDate.getDate() - 4);

const tasks = ref([
    { id: 1, title: 'Task 1', description: 'This is task 1', interval: 2, startDate: startDate1 },
    { id: 2, title: 'Task 2', description: 'This is task 2', interval: 5, startDate: startDate2 },
    { id: 3, title: 'Task 3', description: 'This is task 3', interval: 10, startDate: startDate3 },
    { id: 4, title: 'Task 4', description: 'This is task 4', interval: 15, startDate: startDate4 },
])

function calculateDueDate(task) {
    let reval = new Date(task.startDate);
    reval.setDate(reval.getDate() + task.interval);
    return reval;
}

function finishTask(task) {
    task.startDate = new Date();
}
</script>