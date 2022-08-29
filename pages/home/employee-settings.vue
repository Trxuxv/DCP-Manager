<template>
  <div class="w-full h-full flex items-center justify-center">
    <div class="w-5/6 h-5/6 rounded-lg shadow-2xl  overflow-y-scroll">
      <div class="overflow-x-auto relative">
        <div class="font-medium text-xl my-2 px-4 bg-white">
          Employees
        </div>
        <div class="w-full h-14 py-2 bg-gray-50 flex px-2">
          <label for="simple-search" class="sr-only">Search by name</label>
          <div class="relative w-5/6">
            <div class="flex absolute inset-y-0 left-0 items-center pl-3 pointer-events-none">
              <svg aria-hidden="true" class="w-5 h-5 text-gray-500 dark:text-gray-400" fill="currentColor"
                viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd"
                  d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z"
                  clip-rule="evenodd"></path>
              </svg>
            </div>
            <input type="text" id="simple-search" v-model="search"
              class="bg-gray-100 border focus:outline-none border-gray-300 text-gray-900 text-sm rounded-lg  block w-full pl-10 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white"
              placeholder="Search by name" />
          </div>
          <div class="text-center flex justify-center items-center px-8">
            <p class="font-normal text-sm text-gray-500"> Displaying total of <span class="text-normal">{{ total }}</span> records
            </p>
          </div>
        </div>
        <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
          <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
            <tr>
              <th scope="col" class="py-3 px-6">

              </th>
              <th scope="col" class="py-3 px-6">
                Full Name
              </th>
              <th scope="col" class="py-3 px-6">
                Username
              </th>
              <th scope="col" class="py-3 px-6">
                E-mail
              </th>
              <th scope="col" class="py-3 px-6">
                Phone
              </th>
              <th scope="col" class="py-3 px-6">
                Company
              </th>
            </tr>
          </thead>

          <tbody>
            <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700" v-for="item in filteredEmployees"
              :key="item.id">
              <th scope="row" class="py-4 px-6 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                <img :src="item.image" class="w-10" alt="">
              </th>
              <th scope="row" class="py-4 px-6 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                {{ item?.firstName }} {{ item?.lastName }}
              </th>
              <td class="py-4 px-6">
                {{ item?.username }}
              </td>
              <td class="py-4 px-6">
                {{ item?.email }}
              </td>
              <td class="py-4 px-6">
                {{ item?.phone }}
              </td>
              <td class="py-4 px-6">
                {{ item?.company.name }}
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import Vue from "vue";
import { Employee } from './../../models/employee.model'

export default Vue.extend({
  name: "Emplyees",
  data() {
    return {
      employees: [] as Employee[],
      loading: true,
      search: '',
      total: 0
    };
  },
  created() {
    fetch("https://dummyjson.com/users?skip=5&limit=100")
      .then((response) => response.json())
      .then((data) => {
        console.log(data.users)
        if (typeof window !== 'undefined') {
          localStorage.setItem("employees", JSON.stringify(data))
        }
        (this.employees = data.users), (this.loading = false), (this.total = data.users.length);
      });
  },
  computed: {
    filteredEmployees() {
      let response = this.employees.filter((x) => {
        return x.firstName.toLowerCase().includes(this.search.toLowerCase());
      });

      this.total = response.length;
      return response;
    }
  },
});
</script>
