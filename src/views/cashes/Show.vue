<template>
  <div class="container">
    <div class="w-full lg:w-1/2">
      <div class="overflow-hidden border rounded-lg">
        <div class="p-4 border-b bg-gray-50">
          {{ transaction.name }}
        </div>
        <div class="p-4">
          <div class="mb-4">
            <label class="text-xs tracking-wider text-gray-500 uppercase"
              >Amount</label
            >
            <div class="leading-relaxed">Rp {{ transaction.amount }}</div>
          </div>
          <div class="mb-4">
            <label class="text-xs tracking-wider text-gray-500 uppercase"
              >Stored</label
            >
            <div class="leading-relaxed">{{ transaction.when }}</div>
          </div>
          <div class="mb-4">
            <label class="text-xs tracking-wider text-gray-500 uppercase"
              >Description</label
            >
            <div class="leading-relaxed">{{ transaction.description }}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axios from "axios";
import router from "@/router";
export default {
  setup() {
    const route = useRoute();
    const transaction = ref([]);
    let slug = route.params.slug;

    const getTransaction = async () => {
      try {
        let { data } = await axios.get(`api/cash/${slug}`);
        transaction.value = data.data;
      } catch (error) {
        router.replace("/cashes");
      }
    };

    onMounted(() => {
      getTransaction();
    });

    return {
      transaction,
    };
  },
};
</script>

<style></style>
