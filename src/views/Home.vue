<script setup>
import {ref, onMounted, watch } from 'vue'

const subjects = ref([])
const input_subject = ref('')
const number_of_rows = ref()
const number_of_subjects = ref(0)

const addSubject = () => {
    if(input_subject.value.trim() === '' || input_subject.value === null)
    {
        return
    }

    subjects.value.push({
        id: number_of_subjects.value + 1,
        name: input_subject.value
    })

    input_subject.value = ''
}

const deleteSubject = subject => {
    subjects.value = subjects.value.filter(t => t !== subject)
}


watch(subjects, newVal => {
    localStorage.setItem('subjects', JSON.stringify(newVal))
    number_of_subjects.value = number_of_rows.value = subjects.value.length 
}, { deep: true })

onMounted( () => {
    subjects.value = JSON.parse(localStorage.getItem('subjects')) || []
})


</script>


<template>
    <div class="mb-5">
        <div>
            <form class="space-y-4 md:space-y-6" @submit.prevent="addSubject">
                <div>
                    <label for="name" class="block mb-2 text-xl font-medium text-gray-900 dark:text-white">Input A Subject</label>
                    <input v-model="input_subject" type="text" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Name of Subject" required autofocus>
                </div>
                
                <div class="flex justify-end">
                    <button type="submit" class="text-gray-200 bg-purple-800 hover:bg-purple-900 focus:ring-4 focus:outline-none focus:ring-purple-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-primary-600 dark:hover:bg-purple-900 dark:focus:ring-primary-800">Add</button>
                </div>
            </form>
        </div>

        <div class="overflow-x-auto relative mt-10">
            <table class="w-1/2 mx-auto text-sm text-left text-gray-500 dark:text-gray-400">
                <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
                    <tr>
                        <th scope="col" class="py-3 px-6">
                            id
                        </th>
                        <th scope="col" class="py-3 px-6">
                            Name
                        </th>
                        <th scope="col" class="py-3 px-6">
                            Action
                        </th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="subject in subjects" :key="subject.id" class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                        <td  class="py-4 px-6">
                            {{ subject.id }}
                        </td>
                        <td class="py-4 px-6">
                            <input type="text" v-model="subject.name" class="py-1 px-2 focus:outline-none bg-gray-600 text-gray-200">
                        </td>
                        <td  class="py-4 px-6">
                            <button @click="deleteSubject(subject)" class="text-red-200 bg-red-600 hover:bg-red-700 focus:ring-4 focus:outline-none focus:ring-purple-300 font-medium rounded-lg text-sm px-3 py-1 text-center dark:bg-primary-600 dark:hover:bg-red-800 dark:focus:ring-primary-800">
                                Delete
                            </button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>

        <div class="flex justify-end mt-20">
            <router-link 
                to="/result" 
                class="text-gray-200 bg-purple-800 hover:bg-purple-900 focus:ring-4 focus:outline-none focus:ring-purple-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-primary-600 dark:hover:bg-purple-900 dark:focus:ring-primary-800"
                >
                    Proceed
                </router-link>
        </div>
    </div>
</template>