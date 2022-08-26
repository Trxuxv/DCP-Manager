<template>
  <div class="w-full h-screen">
    <div class="flex">
      <div
        v-show="sideMenu"
        class="w-1/6 h-screen flex flex-col justify-center items-center bg-default"
      >
        <div class="h-2/6 w-full">
          <div
            class="w-full py-4 text-center flex justify-center bg-gray-50 items-center font-bold top-0"
          >
            <img class="w-10" src="./../static/icons/3.png" alt="" />
            DCP Management
          </div>
          <div class="w-full py-4 my-1 mx-2 text-center" v-for="sm in menuSide">
            {{ sm.name }}
          </div>
        </div>
        <div class="h-4/6 w-full"></div>
      </div>
      <div class="w-full h-full">
        <div
          class="w-full h-16 bg-default-light flex-col justify-center items-center relative"
        >
          <div class="w-1/6 h-full flex justify-left items-center float-left">
            <svg
              @click="openMenu()"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-6 h-6 ml-2 cursor-pointer"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5"
              />
            </svg>
          </div>
          <div class="w-5/6 h-full flex justify-center items-center">
            <div class="w-2/6 float-right"></div>
            <div class="w-4/6 float-right flex justify-center items-center">
              <div v-for="m in menu" class="mx-10 text-sm cursor-pointer">
                <NuxtLink :to="`/home/${m.link}`">{{ m.name }}</NuxtLink>
              </div>
            </div>
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                @click="onLogOut()"
                stroke="currentColor"
                class="w-6 h-6 float-right cursor-pointer"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M17.982 18.725A7.488 7.488 0 0012 15.75a7.488 7.488 0 00-5.982 2.975m11.963 0a9 9 0 10-11.963 0m11.963 0A8.966 8.966 0 0112 21a8.966 8.966 0 01-5.982-2.275M15 9.75a3 3 0 11-6 0 3 3 0 016 0z"
                />
              </svg>
            </div>
          </div>
        </div>
        <div class="w-full bg-green-50 child-components flex items-center justify-center">
          Child goes here
          <NuxtChild />
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { MenuModel } from "~/core/menu/models/menu.model";
import { menuSide } from "~/core/menu/menuSide";
import { menu } from "~/core/menu/menu";
import Vue from "vue";

export default Vue.extend({
  name: "Home",
  data() {
    return {
      sideMenu: false,
      menu: menu as MenuModel[],
      menuSide: menuSide as MenuModel[],
    };
  },
  methods: {
    openMenu() {
      this.sideMenu = !this.sideMenu;
    },
    onLogOut() {
      localStorage.clear();
      window.location.reload();
      this.$router.push("/");
    },
  },
});
</script>
<style>
.bg-default {
  background-color: #49978e;
}

.bg-default-light {
  background-color: #49978e7e;
}

.child-components {
  height: 90vh;
}
</style>
