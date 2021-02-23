<template>
  <div class="border-b lg:py-3">
    <div class="flex flex-col justify-between lg:flex-row ">
      <div
        class="flex items-center justify-between px-6 py-4 border-b lg:pr-0 lg:border-0 lg:py-0"
      >
        <router-link
          class="font-semibold uppercase"
          to="/"
          exact-active-class="bg-transparent"
        >
          CashInOut
        </router-link>

        <button
          @click="isOn = !isOn"
          class="block lg:hidden focus:outline-none"
        >
          <svg
            class="w-5 h-5"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              :class="isOn ? 'hidden' : 'block'"
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 6h16M4 12h16m-7 6h7"
            ></path>

            <path
              :class="isOn ? 'block' : 'hidden'"
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M6 18L18 6M6 6l12 12"
            ></path>
          </svg>
        </button>
      </div>
      <div
        :class="isOn ? 'block' : 'hidden'"
        class="flex-col justify-between w-full px-6 py-4 lg:flex lg:flex-row lg:items-center lg:py-0"
      >
        <div class="flex flex-col lg:flex-row lg:items-center">
          <router-link :class="className" to="/about">About</router-link>
          <router-link :class="className" to="/cashes">Cash</router-link>
        </div>
        <div class="flex items-center" v-if="authenticated">
          <router-link :class="className" to="/login">{{
            user.name
          }}</router-link>
          <button @click="logout" :class="className" class="focus:outline-none">
            Logout
          </button>
        </div>
        <div class="flex flex-col lg:flex-row lg:items-center" v-else>
          <router-link :class="className" to="/login">Login</router-link>
          <router-link :class="className" to="/register">Register</router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed } from "vue";
import store from "../store";
export default {
  setup() {
    const className = "px-4 py-2";
    const isOn = ref(false);

    const authenticated = computed(() => store.getters["auth/authenticated"]);
    const user = computed(() => store.getters["auth/user"]);

    const logout = async () => {
      store.dispatch("auth/logout");
    };

    return { className, isOn, authenticated, user, logout };
  },
};
</script>
