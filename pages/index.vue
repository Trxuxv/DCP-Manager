<template>
  <div>
    <div v-show="!isLoggedIn">
      <loginVue />
    </div>
  </div>
</template>

<script lang="ts">
import loginVue from "./auth/login.vue";
import Vue from "vue";

export default Vue.extend({
  name: "IndexPage",
  components: {
    loginVue,
  },
  mounted() {
    this.storage();
    if (this.isLoggedIn) {
      this.$router.push('home')
    }
  },
  data() {
    return {
      isLoggedIn: false
    }
  },
  methods: {
    storage() {
      let session = localStorage.getItem("session");
      session != null ? this.isLoggedIn = true : this.isLoggedIn = false;
    }
  }
});
</script>
