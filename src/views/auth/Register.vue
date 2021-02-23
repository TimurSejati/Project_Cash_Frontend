<template>
  <div class="container">
    <div class="w-full lg:w-1/3">
      <div class="overflow-hidden border rounded-lg">
        <div class="px-4 py-4 border-b border-gray-200 bg-gray-50">
          Register
        </div>
        <div class="p-4">
          <form @submit.prevent="register">
            <div class="mb-5">
              <label
                for="name"
                class="block mb-2 text-xs font-medium uppercase"
              >
                Name
              </label>
              <input
                v-model="form.name"
                type="text"
                name="name"
                id="name"
                class="w-full h-10 px-4 transition duration-200 border rounded-lg focus:outline-none focus:ring focus:border-blue-200"
              />
              <div class="mt-2 text-sm text-red-500" v-if="errors['name']">
                {{ errors["name"][0] }}
              </div>
            </div>

            <div class="mb-5">
              <label
                for="email"
                class="block mb-2 text-xs font-medium uppercase"
              >
                Email
              </label>
              <input
                v-model="form.email"
                type="email"
                name="email"
                id="email"
                class="w-full h-10 px-4 transition duration-200 border rounded-lg focus:outline-none focus:ring focus:border-blue-200"
              />
              <div class="mt-2 text-sm text-red-500" v-if="errors['email']">
                {{ errors["email"][0] }}
              </div>
            </div>

            <div class="mb-5">
              <label
                for="password"
                class="block mb-2 text-xs font-medium uppercase"
              >
                Password
              </label>
              <input
                v-model="form.password"
                type="password"
                name="password"
                id="password"
                class="w-full h-10 px-4 transition duration-200 border rounded-lg focus:outline-none focus:ring focus:border-blue-200"
              />
              <div class="mt-2 text-sm text-red-500" v-if="errors['password']">
                {{ errors["password"][0] }}
              </div>
            </div>

            <div class="mb-5">
              <label
                for="password_confirmation"
                class="block mb-2 text-xs font-medium uppercase"
              >
                Password Confirmation
              </label>
              <input
                v-model="form.password_confirmation"
                type="password"
                name="password_confirmation"
                id="password_confirmation"
                class="w-full h-10 px-4 transition duration-200 border rounded-lg focus:outline-none focus:ring focus:border-blue-200"
              />
            </div>

            <button
              class="h-10 px-4 text-white bg-blue-500 rounded-lg focus:ring focus:ring-blue-300 hover:bg-blue-600"
            >
              Register
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { reactive, ref } from "vue";
import router from "@/router";
import store from "@/store";

export default {
  setup() {
    const errors = ref([]);

    const form = reactive({
      name: "",
      email: "",
      password: "",
      password_confirmation: "",
    });

    const register = async () => {
      try {
        await axios.post("register", form);
        await store.dispatch("auth/me");
        router.replace("/");
      } catch (error) {
        errors.value = error.response.data.errors;
      }
    };

    return { form, register, errors };
  },
};
</script>
