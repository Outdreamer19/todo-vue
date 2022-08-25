<template>
    <div class="bg-gray-200 py-6 sm:py-8 lg:py-12">
  <div class="max-w-screen-2xl px-4 md:px-8 mx-auto">
    <h2 class="text-gray-800 text-2xl lg:text-3xl font-bold text-center mb-4 md:mb-8">Login</h2>

    <form class="bg-white max-w-lg border rounded-lg mx-auto">
        <div class="flex flex-col gap-4 p-4 md:p-8">
            <div>
                <label for="email" class="inline-block text-gray-800 text-sm sm:text-base mb-2">Tasks</label>
                <input v-model="task" name="text" placeholder="Enter task" class="w-full bg-gray-50 text-gray-800 border focus:ring ring-indigo-300 rounded outline-none transition duration-100 px-3 py-2" />
            </div>
            
            <button @click="submitTask" type="button" class="inline-flex justify-center px-2.5 py-1.5 border border-transparent text-xs font-medium rounded shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">Create</button>
        </div>
        <div class="px-4 sm:px-6 lg:px-8">
        
        <div class="-mx-4 mt-0 mb-5 overflow-hidden shadow ring-1 ring-black ring-opacity-5 sm:-mx-6 md:mx-0 md:rounded-lg">
        <table class="min-w-full divide-y divide-gray-300 text-center">
            <thead class="bg-gray-50">
            <tr class="text-center">
                <th scope="col" class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-6">Name</th>
                <th scope="col" class=" px-3 py-3.5 text-left text-sm font-semibold text-gray-900 lg:table-cell">Title</th>
                <th scope="col" class=" px-3 py-3.5 text-left text-sm font-semibold text-gray-900 sm:table-cell">Email</th>
                <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">Role</th>
                
            </tr>
            </thead>
            <tbody class="divide-y divide-gray-200 bg-white">
           <tr v-for="(task, index) in tasks" :key="index">
               <td>{{task.name}}</td>
               <td>{{task.status}}</td>
               <td class="text-center">
                   <svg class="text-center" @click="editTask(index)" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="orange" width="1.5em" height="1.5em"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15.232 5.232l3.536 3.536m-2.036-5.036a2.5 2.5 0 113.536 3.536L6.5 21.036H3v-3.572L16.732 3.732z"></path></svg>
               </td>
               <td>
                   <svg class="text-center" @click="deleteTask(index)" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="red" width="1.5em" height="1.5em"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path></svg>
                   
                </td>
           </tr>
            </tbody>
        </table>
        </div>
        </div>

    </form>
    <!-- This example requires Tailwind CSS v2.0+ -->


  </div>
</div>
</template>
<script>
export default {
    name: "Todo",
    props: {
        msg: String,
    },

    data(){
        return {
            task: '',
            editedTask: null,
            availableStatuses: ['to-do', 'in-progress',, 'finished'],
            tasks: [
                {
                    name: 'Steal bananas.',
                    status: 'to-do'
                },
                {
                    name: 'Eat chocolate.',
                    status: 'in-progress'
                }
            ]
        }
    },

    methods: {
        submitTask(){
            if (this.task.length === 0) return;

            if (this.editedTask === null){
                this.tasks.push({
                    name: this.task,
                    status: 'To-do'
                });
                
            }else {
                this.tasks[this.editedTask].name = this.task;
                this.editedTask = null;
            }
            this.task = '';
        },

        deleteTask(index){
            this.tasks.splice(index, 1);
        },
        
        editTask(index){
           this.task =  this.tasks[index].name;
           this.editedTask = index;
        }
    }
};
</script>