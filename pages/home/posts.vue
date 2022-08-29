<template>
  <div class="w-full h-full flex flex-col items-center justify-center">
    <div class="w-full h-16 flex items-center justify-center text-right shadow-2xl">
      Posts
    </div>
    <div class="w-full h-full flex justify-center items-center" v-show="loading">
      <svg role="status" class="inline mr-2 w-16 h-16 text-gray-200 animate-spin dark:text-gray-600" viewBox="0 0 100 101"
        fill="none" xmlns="http://www.w3.org/2000/svg">
        <path
          d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z"
          fill="currentColor"></path>
        <path
          d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z"
          fill="green"></path>
      </svg>
    </div>
    <div class="w-full h-full overflow-y-scroll" v-show="!loading">
      <div class="grid grid-cols-4 gap-5 w-5/6 py-10 mx-auto">
        <div v-for="item in innerData" :key="item.id" v-show="item.user"
          class="max-w-sm bg-white rounded-lg border border-gray-200 shadow-md dark:bg-gray-800 dark:border-gray-700">
          <a href="#">
            <img :src="item?.image?.download_url" class="h-64" />
          </a>
          <div class="p-5">
            <div class="flex justify-center items-center w-full h-16">
              <div class="w-12 text-right">
                <img :src="item?.user?.image" class="w-10 bg-green-100 rounded-full" alt="" />
              </div>
              <div class="w-4/5 text-left">
                {{ item?.user?.firstName }} {{ item?.user?.lastName }}
              </div>
            </div>
            <a href="#">
              <h5 class="mb-2 text-xl font-bold tracking-tight text-gray-900 dark:text-white h-14 py-2">
                {{ item?.title }}
              </h5>
            </a>
            <div v-show="!readmore">
              <p class="mb-3 font-normal text-gray-700 dark:text-gray-400 overflow-hidden h-20 text-sm">
                {{ item?.body.substring(0, 200) + "..." }}
              </p>
              <div>
                <a href="#" @click="OnReadMore(item?.id)"
                  class="inline-flex items-center py-2 px-3 text-sm font-medium text-center text-white bg-green-700 rounded-lg hover:bg-green-800 focus:ring-4 focus:outline-none focus:ring-green-300 dark:bg-green-600 dark:hover:bg-green-700 dark:focus:ring-green-800">
                  Read more
                  <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                    stroke="currentColor" class="ml-2 -mr-1 w-4 h-4">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 13.5L12 21m0 0l-7.5-7.5M12 21V3" />
                  </svg>
                </a>
              </div>
            </div>
            <div v-show="readmore" class="flex flex-col bg-white ">
              <div class=" h-4/6 pb-16 pt-2">
                <p class="mb-3 font-normal text-gray-700 dark:text-gray-400 h-20 text-sm">
                  {{ item?.body }}
                </p>
              </div>
              <div class="mt-5 text-center h-1/6">
                <a href="#"
                  class="inline-flex items-center py-2 px-3 text-sm font-medium text-center text-white bg-green-700 rounded-lg hover:bg-green-800 focus:ring-4 focus:outline-none focus:ring-green-300 dark:bg-green-600 dark:hover:bg-green-700 dark:focus:ring-green-800"
                  @click="OnReadMore(item?.id)">
                  Read less
                  <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                    stroke="currentColor" class="ml-2 -mr-1 w-4 h-4">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M4.5 10.5L12 3m0 0l7.5 7.5M12 3v18" />
                  </svg>
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { Employee } from "~/models/employee.model";
import { Image } from "~/models/image.motel";
import { Post } from "~/models/post.model";
import Vue from "vue";

export default Vue.extend({
  name: "Post",
  data() {
    return {
      posts: [] as Post[],
      loading: true,
      search: "",
      divOpen: 0,
      readmore: false,
      images: [] as Image[],
      users: [] as Employee[],
    };
  },
  created() {
    fetch("https://dummyjson.com/posts?skip=5&limit=100")
      .then((response) => response.json())
      .then((data) => {
        if (typeof window !== "undefined") {
          localStorage.setItem("posts", JSON.stringify(data));
        }
        (this.posts = data.posts), (this.loading = false);
      });

    fetch("https://dummyjson.com/users?skip=5&limit=100")
      .then((response) => response.json())
      .then((data) => {
        if (typeof window !== "undefined") {
          localStorage.setItem("posts", JSON.stringify(data));
        }
        (this.users = data.users), (this.loading = false);
      });

    fetch("https://picsum.photos/v2/list?page=2&limit=100")
      .then((response) => response.json())
      .then((data) => {
        (this.images = data), (this.loading = false);
      });
  },
  computed: {
    innerData() {
      for (var i = 0; i < this.images.length; i++) {
        var obj = this.images[i]
        obj.id = String(i);
      }

      return this.posts.map((post) => {
        this.loading = false;
        const user = this.users.find((user) => post.userId === user.id);
        const image = this.images.find((img) => post.id === Number(img.id))
        return { ...post, user, image };
      });
    },
  },
  methods: {
    OnReadMore(id: number) {
      this.divOpen = id;
      this.readmore = !this.readmore;
    }
  }
});
</script>
