<script setup>
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <h1 class="text-gray-200 text-center text-3xl my-10 font-bold uppercase">Result Checker</h1>

  <div class="flex items-center w-11/12 mb-5 mx-auto justify-between">
    <div>
      <h2 class="text-gray-300 font-semibold text-xl mb-3">Order By</h2>
      <div class="flex space-x-5">
        <button class="bg-purple-800 rounded-md px-5 py-2 dark:text-gray-200 font-semibold hover:bg-purple-900">
          Alphabetical Order
        </button>
        <button class="bg-purple-800 rounded-md px-5 py-2 dark:text-gray-200 font-semibold hover:bg-purple-900">
          Position
        </button>
      </div>
    </div>
    <button class="bg-purple-800 rounded-md px-5 py-3 dark:text-gray-200 font-semibold hover:bg-purple-900">
      Export Excel
    </button>
  </div>

<div class="overflow-x-auto w-11/12 mx-auto relative shadow-md sm:rounded-lg">
    <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
        <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-300">
            <tr>
                <th scope="col" class="py-3 px-6">
                    Name
                </th>
                <th scope="col" class="py-3 px-6">
                    English
                </th>
                <th scope="col" class="py-3 px-6">
                    Mathematics
                </th>
                <th scope="col" class="py-3 px-6">
                    Biology
                </th>
                <th scope="col" class="py-3 px-6">
                    Chemistry
                </th>
                <th scope="col" class="py-3 px-6">
                    Physics
                </th>
                <th scope="col" class="py-3 px-6">
                    Geography
                </th>
                <th scope="col" class="py-3 px-6">
                    Civic Education
                </th>
                <th scope="col" class="py-3 px-6">
                    Further Mathematics
                </th>
                <th scope="col" class="py-3 px-6">
                    Catering
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
                    John Doe
                </th>
                <td class="py-4 px-6">
                    78
                </td>
                <td class="py-4 px-6">
                    87
                </td>
                <td class="py-4 px-6">
                    79
                </td>
                <td class="py-4 px-6">
                    84
                </td>
                <td class="py-4 px-6">
                    93
                </td>
                <td class="py-4 px-6">
                    80
                </td>
                <td class="py-4 px-6">
                    88
                </td>
                <td class="py-4 px-6">
                    84
                </td>
                <td class="py-4 px-6">
                    63
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
            <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 dark:text-gray-300">
                <th scope="row" class="py-4 px-6 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                    John Doe
                </th>
                <td class="py-4 px-6">
                    78
                </td>
                <td class="py-4 px-6">
                    87
                </td>
                <td class="py-4 px-6">
                    79
                </td>
                <td class="py-4 px-6">
                    84
                </td>
                <td class="py-4 px-6">
                    93
                </td>
                <td class="py-4 px-6">
                    80
                </td>
                <td class="py-4 px-6">
                    88
                </td>
                <td class="py-4 px-6">
                    84
                </td>
                <td class="py-4 px-6">
                    63
                </td>
                <td class="py-4 px-6">
                  720
                </td>
                <td class="py-4 px-6">
                    80.23
                </td>
                <td class="py-4 px-6">
                    3rd
                </td>
                <td class="py-4 px-6">
                    <a href="#" class="font-medium text-blue-600 dark:text-blue-500 hover:underline">Edit</a>
                </td>
            </tr>
            <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 dark:text-gray-300">
                <th scope="row" class="py-4 px-6 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                    John Doe
                </th>
                <td class="py-4 px-6">
                    78
                </td>
                <td class="py-4 px-6">
                    87
                </td>
                <td class="py-4 px-6">
                    79
                </td>
                <td class="py-4 px-6">
                    84
                </td>
                <td class="py-4 px-6">
                    93
                </td>
                <td class="py-4 px-6">
                    80
                </td>
                <td class="py-4 px-6">
                    88
                </td>
                <td class="py-4 px-6">
                    84
                </td>
                <td class="py-4 px-6">
                    63
                </td>
                <td class="py-4 px-6">
                  720
                </td>
                <td class="py-4 px-6">
                    60.23
                </td>
                <td class="py-4 px-6">
                    4th
                </td>
                <td class="py-4 px-6">
                    <a href="#" class="font-medium text-blue-600 dark:text-blue-500 hover:underline">Edit</a>
                </td>
            </tr>
            <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 dark:text-gray-300">
                <th scope="row" class="py-4 px-6 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                    John Doe 3
                </th>
                <td class="py-4 px-6">
                    78
                </td>
                <td class="py-4 px-6">
                    87
                </td>
                <td class="py-4 px-6">
                    79
                </td>
                <td class="py-4 px-6">
                    84
                </td>
                <td class="py-4 px-6">
                    93
                </td>
                <td class="py-4 px-6">
                    80
                </td>
                <td class="py-4 px-6">
                    88
                </td>
                <td class="py-4 px-6">
                    84
                </td>
                <td class="py-4 px-6">
                    63
                </td>
                <td class="py-4 px-6">
                  720
                </td>
                <td class="py-4 px-6">
                    78.3
                </td>
                <td class="py-4 px-6">
                    2nd
                </td>
                <td class="py-4 px-6">
                    <a href="#" class="font-medium text-blue-600 dark:text-blue-500 hover:underline">Edit</a>
                </td>
            </tr>
        </tbody>
    </table>
</div>


</template>

