<template>
  <div class="h-full flex w-full items-center justify-center">
    <div>
    </div>
    <div class="vector-index w-3/4 h-full">
    </div>
    <div class="bg-white w-2/4 h-full flex flex-col justify-center items-center">
      <div class="w-4/5">
        <h1 class="text-6xl font-black flex flex-col py-5 text-center">
          Manage your company
        </h1>
        <p class=" text-center p-5">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Minima hic debitis enim totam, possimus eum nemo
          quisquam neque, numquam beatae quibusdam, id magni ipsa odio nulla asperiores quis amet sequi.
        </p>
        <div class="text-center py-5 flex">
          <div class="w-2/4 text-center">
           <NuxtLink to="dashboard">
            <button type="button"
              class="text-white bg-gradient-to-br from-green-400 to-blue-600 hover:bg-gradient-to-bl focus:ring-4 focus:outline-none focus:ring-green-200 dark:focus:ring-green-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2">
              Dashboard</button>
           </NuxtLink>
          </div>
          <div class="w-2/4">
           <NuxtLink to="settings">
            <button type="button"
              class="text-white bg-gradient-to-br from-pink-500 to-yellow-600 hover:bg-gradient-to-bl focus:ring-4 focus:outline-none focus:ring-pink-200 dark:focus:ring-pink-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2">Settings</button>
           </NuxtLink>
          </div>
        </div>
      </div>
      <div class="h-1/5">
        </div>
    </div>
  </div>
</template>


<style>
.vector-index {
  background-image: url('./../../static/vectors/2.jpg');
  background-size: cover;
}
</style>
