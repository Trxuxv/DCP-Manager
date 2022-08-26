<template>
  <div>
    <div class="flex justify-center items-center h-screen w-full">
      <div class="w-1/3 h-full flex flex-col c-default">
        <div class="w-full flex justify-center items-center h-5/6 px-6">
          <div
            class="w-full bg-white rounded-lg shadow dark:border md:mt-0 sm:max-w-md xl:p-0 dark:bg-gray-800 dark:border-gray-700">
            <a href="#"
              class="flex items-center pt-4 text-center justify-center text-2xl font-semibold text-gray-900 dark:text-white">
              <img class="w-8 h-8 mr-2" src="./../../static/icons/2.jpg" alt="logo" />
              DCP Manager
            </a>
            <div class="p-4 space-y-4 md:space-y-6 sm:p-8">
              <h1 class="text-xl font-bold leading-tight tracking-tight text-gray-900 md:text-2xl dark:text-white">
                Sign in to your account
              </h1>
              <form class="space-y-4 md:space-y-6" action="#">
                <div>
                  <label for="email" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Your
                    email</label>
                  <input type="email" name="email" id="email" v-model="login"
                    class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                    placeholder="name@company.com" required="" />
                </div>
                <div>
                  <label for="password"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Password</label>
                  <input v-model="password" type="password" name="password" id="password" placeholder="••••••••"
                    class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                    required="" />
                </div>
                <div class="flex items-center justify-between">
                  <div class="flex items-start">
                    <div class="flex items-center h-5">
                      <input id="remember" aria-describedby="remember" type="checkbox"
                        class="w-4 h-4 border border-gray-300 rounded bg-gray-50 focus:ring-3 focus:ring-primary-300 dark:bg-gray-700 dark:border-gray-600 dark:focus:ring-primary-600 dark:ring-offset-gray-800"
                        required="" />
                    </div>
                    <div class="ml-3 text-sm">
                      <label for="remember" class="text-gray-500 dark:text-gray-300">Remember me</label>
                    </div>
                  </div>
                  <a href="#" class="text-sm font-medium text-primary-600 hover:underline dark:text-primary-500">Forgot
                    password?</a>
                </div>
                <button type="button" @click="onSignIn()"
                  class="focus:outline-none text-white w-full bg-button hover:bg-green-800 focus:ring-4 focus:ring-green-300 font-medium rounded-lg text-sm px-5 py-2.5 mb-2 dark:bg-green-600 dark:hover:bg-green-700 dark:focus:ring-green-900">
                  Sign in
                </button>
                <p class="text-sm font-light text-gray-500 dark:text-gray-400">
                  Don’t have an account yet?
                  <a href="#" class="font-medium text-primary-600 hover:underline dark:text-primary-500">Sign up</a>
                </p>
              </form>
            </div>
          </div>
        </div>
      </div>
      <div class="w-2/3 h-full bg-blue-200 bg-image"></div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "Login",
  data() {
    return {
      login: "",
      password: "",
      validation: false,
    };
  },
  methods: {
    onSignIn() {
      var d = new Date().getTime();
      let session = "xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx".replace(/[xy]/g, function (c) {
        var r = (d + Math.random() * 16) % 16 | 0;
        d = Math.floor(d / 16);
        return (c === "x" ? r : (r & 0x3) | 0x8).toString(16);
      });
      this.login && this.password != null ? localStorage.setItem("session", session) : this.validation = false;

      window.location.reload();
    },
  },
});
</script>
<style>
.bg-image {
  background-image: url("./../../static/vectors/1.jpg");
  background-size: contain;
}

.c-default {
  background-color: #62bdb1;
}

.bg-button {
  background-color: #49978e;
}
</style>
