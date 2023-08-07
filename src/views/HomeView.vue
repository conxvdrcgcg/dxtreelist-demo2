<script lang="ts">
import { defineComponent, onMounted, ref, computed } from "vue";
import { faker } from "@faker-js/faker";
import DataTable from "@/components/DataTable.vue";

export default defineComponent({
  components: {
    DataTable,
  },
  setup() {
    const dataTableItems = ref<any[]>();
    const isLoading = ref<boolean>(false);

    async function getData() {
      dataTableItems.value = await fakeData();
    }

    function fakeData(): Promise<any[]> {
      return new Promise((resolve) => {
        const items = [];
        for (let i = 0; i < 10000; i++) {
          items.push({
            id: i,
            name: faker.company.name(),
            A: faker.finance.bitcoinAddress(),
            B: faker.finance.accountNumber(),
            C: faker.finance.currencySymbol(),
            D: faker.finance.amount(),
            E: faker.finance.amount(),
            F: faker.finance.amount(),
            G: faker.finance.amount(),
            H: faker.finance.amount(),
            I: faker.finance.amount(),
            J: faker.finance.amount(),
            K: faker.finance.amount(),
            L: faker.finance.amount(),
            M: faker.finance.amount(),
            N: faker.finance.amount(),
            O: faker.finance.amount(),
            P: faker.finance.amount(),
            Q: faker.finance.amount(),
            R: faker.finance.amount(),
            S: faker.finance.amount(),
            T: faker.finance.amount(),
            U: faker.finance.amount(),
            V: faker.finance.amount(),
            W: faker.finance.amount(),
            X: faker.finance.amount(),
            Y: faker.finance.amount(),
            Z: faker.finance.amount(),
          });
        }
        resolve(items);
      });
    }

    onMounted(async () => {
      isLoading.value = true;
      await getData();
      isLoading.value = false;
    });

    return {
      dataTableItems,
      isLoading,
      getData,
      fakeData,
    };
  },
});
</script>

<template>
  <div>
    <h1>Data Table test</h1>
    <button
      v-if="dataTableItems?.length > 0"
      :disabled="isLoading"
      @click="getData"
    >
      Re-fetch Data
    </button>
    <DataTable :items="dataTableItems" />
  </div>
</template>
