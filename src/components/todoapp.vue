<template>
    <div class="flex justify-center mx-2 sm:mx-2 md:mx-0 content-center text-center">

        <!-- Input field -->
        <div class="w-full mt-10 max-w-3xl">
            <div class="flex ">
                <input type="text" v-model="task"
                    class="border-gray-900 appearance-none text-sm border-2 w-full py-2 px-2 md:px-6 dark:text-gray-600 leading-tight focus:outline-none focus:shadow-outline"
                    placeholder="Enter task" required>
                <button
                    class="flex-shrink-0 bg-gray-900 text-white focus:outline-none focus:shadow-outline font-semibold px-4 py-2" @click="submitTask">submit</button>
            </div>

            <!-- Task Table -->
            <div class="relative overflow-x-auto mt-12">
                <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
                    <thead class="text-xs text-gray-700 uppercase bg-white ">
                        <tr class="bg-gray-700 text-md dark:bg-gray-900 font-semibold text-gray-200">
                            <th scope="col" class="px-6 py-3">Tasks</th>
                            <th scope="col" class="px-6 py-3">Status</th>
                            <th scope="col" class="px-6 py-3">#</th>
                            <th scope="col" class="px-6 py-3">#</th>
                        </tr>
                    </thead>
                    <tbody>

                        <tr v-for="(task, index) in tasks" :key="index"
                            class="bg-white border-b text-sm font-thin dark:text-gray-600">
                            <td class="px-6 py-4">
                                <span :class="{ 'line-through': task.status === 'finished' }">
                                    {{ task.name }}
                                </span>
                            </td>
                            <td class="px-6 py-4">
                                <span class="cursor-pointer" @click="changeStatus(index)" :class="{
                                    'text-red-700': task.status === 'to-do',
                                    'text-green-700': task.status === 'finished',
                                    'text-yellow-900': task.status === 'in-progress',
                                }">
                                    {{ capitalizeFirstChar(task.status) }}
                                </span>
                            </td>
                            <td class="px-6 py-4">
                                <div @click="editTask(index)">
                                    <p class="fa fa-pen"></p>
                                </div>
                            </td>
                            <td class="px-6 py-4">
                                <div @click="deleteTask(index)">
                                    <p class="fa fa-trash"></p>
                                </div>
                            </td>
                        </tr>

                    </tbody>
                </table>
            </div>

        </div>
    </div>
</template>

<script>
export default {
    name: 'todoApp',
    props: {
        msg: String,
    },

    data() {
        return {
            task: "",
            editedTask: null,
            Statuses: ["to-do", "in-progress", "finished"],

            tasks: [
                {
                    name: "flamingo Community",
                    status: "to-do",
                },
                {
                    name: "subscribe now",
                    status: "in-progress",
                },
                {
                    name: "Click that button",
                    status: "finished",
                },
            ],
        };
    },
    methods: {
        capitalizeFirstChar(str) {
            return str.charAt(0).toUpperCase() + str.slice(1);
        },
        changeStatus(index) {
            let newIndex = this.statuses.indexOf(this.tasks[index].status);
            if (++newIndex > 2) newIndex = 0;
            this.tasks[index].status = this.statuses[newIndex];
        },
        // delete task by index
        deleteTask(index) {
            this.tasks.splice(index, 1);
        },

        // edit task
        editTask(index) {
            this.task = this.tasks[index].name;
            this.editedTask = index;
        },

        // subit task
        submitTask() {
            if (this.task.length === 0) return;

            if (this.editedTask != null) {
                this.tasks[this.editedTask].name = this.task;
                this.editedTask = null;
            } else {
                this.tasks.push({
                    name:this.task,
                    status:"todo",
                });
            }
            this.task = "";
        },
    },
};
</script>

<style scoped>
* {
    /* border: 1px solid red; */
    font-family:  'Fira Code', monospace;
}
</style>