<template>
    <div>
        <h1 class="mb-4 text-3xl font-extrabold text-gray-900 dark:text-white md:text-5xl lg:text-6xl"><span class="text-transparent bg-clip-text bg-gradient-to-r to-emerald-600 from-sky-400">Mis tareas app</span></h1>     
        <form  @submit.prevent="createTask">
            <div class="mb-6">
                <h6 class="text-left text-lg font-bold dark:text-white">Agregar una nueva tarea</h6>
                <input type="text" v-model="newTask" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
            </div>
            <button type="submit" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Submit</button>
        </form>
        <h6 v-if="tasks.length > 0" class="text-left text-lg font-bold dark:text-white">Lista de pendientes</h6>
        <ul>
            <li
                v-for="(task, i) in tasks"
                :key="'task' + i"
                class="text-left"
            >
            <div
            @click="completeTask(task.name)" 
            :class="{
                'bg-green-50 text-green-800': !task.done,
                'bg-red-50 text-red-800': task.done,
                'p-4 mb-4 text-sm rounded-lg dark:bg-gray-800 dark:text-green-400 role=alert' : true
                }"
            >
                <span class="font-medium">{{ task.name }}</span> 
            </div>
            </li>
        </ul>
    </div>
</template> 

<script>
    export default {
        name: 'TodoList',
        data() {
            return {
                newTask: '',
                tasks: []
            }
        },
        methods: {
                createTask() {
                    if(this.newTask.trim() !== ''){
                        let task = {
                        name: this.newTask,
                        done: false
                        }  
                        this.tasks.push(task);
                        this.newTask = '';
                    }
                },
                completeTask(taskText) {
                    const taskToUpdate = this.tasks.find(task => task.name === taskText);
                        if (taskToUpdate) {
                            taskToUpdate.done = !taskToUpdate.done;
                        }
                }  
            }
    };
</script>