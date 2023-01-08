<script setup>
import HelloWorld from './components/HelloWorld.vue'
import {ref, onMounted, computed, watch } from 'vue'

const firstPage = ref(true);
const subjects = ref([])
const individual_reports = ref([])
const name = ref()
const score = ref([])
const input_subject = ref('')
const number_of_subjects = ref(0)
const subjects_name = ref([])

const i = ref(1);

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

const addColumn = () => {

    subjects_name.value = subjects.value.map(({name}) => name)

    individual_reports.value.push({
        name: name.value,
        subjects: subjects_name.value,
        scores: score.value
    })

    console.log(individual_reports.value)
}


watch(subjects, newVal => {
    localStorage.setItem('subjects', JSON.stringify(newVal))
     number_of_subjects.value = subjects.value.length
}, { deep: true })

watch(individual_reports, newVal => {
    localStorage.setItem('individual_reports', JSON.stringify(newVal))
}, {deep: true })

onMounted( () => {
    subjects.value = JSON.parse(localStorage.getItem('subjects')) || []
})


</script>

<template>
  <h1 class="text-gray-200 text-center text-3xl my-10 font-bold uppercase">Result Checker</h1>

<div class="w-11/12 mx-auto">
    <div v-if="firstPage" class="mb-5">
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
                            <button class="text-red-200 bg-red-600 hover:bg-red-700 focus:ring-4 focus:outline-none focus:ring-purple-300 font-medium rounded-lg text-sm px-3 py-1 text-center dark:bg-primary-600 dark:hover:bg-red-800 dark:focus:ring-primary-800">
                                Delete
                            </button>
                        </td>
                    </tr>
                </tbody>
            </table>

            <div class="flex justify-end mt-20">
                <button @click="firstPage = !firstPage" class="text-gray-200 bg-purple-800 hover:bg-purple-900 focus:ring-4 focus:outline-none focus:ring-purple-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-primary-600 dark:hover:bg-purple-900 dark:focus:ring-primary-800">
                    Proceed
                </button>
            </div>
        </div>
    </div>

    <div v-if="!firstPage">
        <div class="flex items-center w-full mb-5 mx-auto justify-between">
            <div>
                <h2 class="text-gray-300 font-semibold text-xl mb-3">Order By</h2>
                <div class="flex space-x-5">
                    <button class="bg-purple-800 rounded-md px-5 py-2 dark:text-gray-200 font-semibold hover:bg-purple-900">
                        Alphabetical Order
                    </button>
                    <button @click="testing" class="bg-purple-800 rounded-md px-5 py-2 dark:text-gray-200 font-semibold hover:bg-purple-900">
                        Position
                    </button>
                </div>
            </div>
            <button class="bg-purple-800 rounded-md px-5 py-3 dark:text-gray-200 font-semibold hover:bg-purple-900">
                Export Excel
            </button>
        </div>

        <div class="overflow-x-auto w-full mx-auto relative shadow-md sm:rounded-lg">
            <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
                <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-300">
                    <tr>
                        <th scope="col" class="py-3 px-6">
                            Name
                        </th>
                        <th v-for="subject in subjects" :key="subject.id" scope="col" class="py-3 px-6">
                            {{ subject.name }}
                        </th>
                        <th scope="col" class="py-3 px-6">
                            Total
                        </th>
                        <th scope="col" class="py-3 px-6">
                            Average
                        </th>
                        <th scope="col" class="py-3 px-6">
                            Position
                        </th>
                        <th scope="col" class="py-3 px-6">
                            Actions
                        </th>
                    </tr>
                </thead>
                <tbody>
                    <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 dark:text-gray-300">
                        <th scope="row" class="py-4 px-6 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                            <input type="text" v-model="name" class="py-1 px-2 focus:outline-none bg-gray-600 text-gray-200">
                        </th>
                        <td v-for="(n, index) in number_of_subjects" :key="n" class="py-4 px-6">
                            <input type="text" v-model="score[index]" class="py-1 px-2 focus:outline-none bg-gray-600 text-gray-200"> 
                        </td>
                        <td class="py-4 px-6">
                            720
                        </td>
                        <td class="py-4 px-6">
                            80.23
                        </td>
                        <td class="py-4 px-6">
                            1st
                        </td>
                        <td class="py-4 px-6">
                            <a href="#" class="font-medium text-blue-600 dark:text-blue-500 hover:underline">Edit</a>
                        </td>
                    </tr>
                </tbody>
            </table>            
        </div>

        <div class="mt-10 flex justify-between">
            <button @click="firstPage = !firstPage" class="text-gray-200 bg-purple-800 hover:bg-purple-900 focus:ring-4 focus:outline-none focus:ring-purple-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-primary-600 dark:hover:bg-purple-900 dark:focus:ring-primary-800">
                Previous
            </button>

            <button @click="addColumn" class="text-gray-200 bg-purple-800 hover:bg-purple-900 focus:ring-4 focus:outline-none focus:ring-purple-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-primary-600 dark:hover:bg-purple-900 dark:focus:ring-primary-800">
                Add New Column
            </button>
        </div> 
    </div>

</div>

</template>