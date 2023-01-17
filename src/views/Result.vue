<script setup>
import {ref, onMounted, watch } from 'vue'

const name = ref([])
const subjects = ref([])
const scores = ref([])
const number_of_columns =  ref()
const number_of_rows = ref()
const splice =  ref()
const total = ref([])
const average = ref([])
const ranking = ref([])
const position = ref([])

function rankings(arr){
  // add whatever parameters you deem necessary....good luck! 
  var sorted = arr.slice().sort(function(a,b){return b-a})
  var ranks = arr.slice().map(function(v){ return sorted.indexOf(v) + 1});
  return ranks;
}

function ordinal_suffix_of(i) {
    var j = i % 10,
        k = i % 100;
    if (j == 1 && k != 11) {
        return i + "st";
    }
    if (j == 2 && k != 12) {
        return i + "nd";
    }
    if (j == 3 && k != 13) {
        return i + "rd";
    }
    return i + "th";
}

const addColumn = () => {
    number_of_columns.value++

    scores.value.push([])

    if(scores.value.length != number_of_columns.value+1){
        splice.value = number_of_columns.value - (scores.value.length-1)
        scores.value.splice(splice.value)
    }
}

const calculate = () => {
    for (let index = 0; index < scores.value.length; index++) {
        total.value[index] = scores.value[index].reduce((a, b) => a + b, 0)
        average.value[index] = Number((total.value[index] / scores.value[index].length).toFixed(2))
    }
    ranking.value = rankings(average.value)
    for (let index = 0; index < ranking.value.length; index++) {
        position.value[index] = ordinal_suffix_of(ranking.value[index])
    }
}

const clearTable = () => {

    localStorage.removeItem('name')
    localStorage.removeItem('scores')
    localStorage.removeItem('total')
    localStorage.removeItem('average')
    localStorage.removeItem('position')

    location.reload();
}

const clearAll = () => {
    localStorage.clear()
}

watch(subjects, newVal => {
    localStorage.setItem('subjects', JSON.stringify(newVal))
     number_of_rows.value = subjects.value.length
}, { deep: true })

watch(name, newVal => {
    localStorage.setItem('name', JSON.stringify(newVal))
    number_of_columns.value = name.value.length
}, {deep: true })

watch(scores, newVal => {
    localStorage.setItem('scores', JSON.stringify(newVal))
}, { deep: true })

watch(total, newVal => {
    localStorage.setItem('total', JSON.stringify(newVal))
}, { deep: true })

watch(average, newVal => {
    localStorage.setItem('average', JSON.stringify(newVal))
}, { deep: true })

watch(position, newVal => {
    localStorage.setItem('position', JSON.stringify(newVal))
}, { deep: true })

onMounted( () => {
    subjects.value = JSON.parse(localStorage.getItem('subjects')) || []
    name.value = JSON.parse(localStorage.getItem('name')) || []
    scores.value = JSON.parse(localStorage.getItem('scores')) || [[]]
    total.value = JSON.parse(localStorage.getItem('total')) || []
    average.value = JSON.parse(localStorage.getItem('average')) || []
    position.value = JSON.parse(localStorage.getItem('position')) || []
})
</script>

<template>
    <div>
        <div class="flex items-center w-full mb-5 mx-auto justify-between">
            <div>
                <div class="flex space-x-5">
                    <router-link 
                        to="/"
                        class="bg-purple-800 rounded-md px-5 py-2 dark:text-gray-200 font-semibold hover:bg-purple-900"
                    >
                        Home
                    </router-link>
                </div>
            </div>
            <button @click="clearTable" class="bg-purple-800 rounded-md px-5 py-3 dark:text-gray-200 font-semibold hover:bg-purple-900">
                Clear Table
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
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(n, index) in number_of_columns" :key="n" class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 dark:text-gray-300 font-semibold">
                        <th scope="row" class="py-4 px-6 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                            <input type="text" v-model="name[index]" placeholder="Input Full Name" class="p-2 focus:outline-none bg-gray-600 text-gray-200 font-bold  tracking-wider">
                        </th>
                        <td v-for="(i, k) in number_of_rows" :key="i">
                            <input type="text" v-model.number="scores[index][k]" placeholder="NULL" class="p-1 md:p-2 focus:outline-none bg-gray-600 text-gray-200 font-semibold">
                        </td>
                        <td class="py-4 px-6">
                            {{ total[index] }}
                        </td>
                        <td class="py-4 px-6">
                            {{ average[index] }}
                        </td>
                        <td class="py-4 px-6">
                            {{ position[index] }}
                        </td>
                    </tr>
                </tbody>
            </table>            
        </div>

        <div class="mt-10 flex justify-between">
            <button @click="calculate" class="text-gray-200 bg-purple-800 hover:bg-purple-900 focus:ring-4 focus:outline-none focus:ring-purple-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-primary-600 dark:hover:bg-purple-900 dark:focus:ring-primary-800">
                Calculate
            </button>

            <button @click="addColumn" class="text-gray-200 bg-purple-800 hover:bg-purple-900 focus:ring-4 focus:outline-none focus:ring-purple-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-primary-600 dark:hover:bg-purple-900 dark:focus:ring-primary-800">
                Add New Column
            </button>
        </div>

        <div 
            class="mt-28 flex justify-center"
        >
            <router-link 
                @click="clearAll" 
                to="/"
                class="bg-red-800 text-gray-100 text-semibold tracking-wider p-4 rounded-md" 
            >Clear Everything</router-link>
        </div>
    </div>
</template>