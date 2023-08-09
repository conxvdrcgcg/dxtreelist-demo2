<script lang="ts">
import { defineComponent, onMounted, ref, computed } from "vue";
import { faker } from "@faker-js/faker";
import DataTable from "@/components/DataTable.vue";
import CustomStore from "devextreme/data/custom_store";

export default defineComponent({
  components: {
    DataTable,
  },
  setup() {
    const dataSource = ref<CustomStore>();
    const isLoading = ref<boolean>(false);
    const componentKey = ref<number>(0);

    async function getData() {
      dataSource.value = new CustomStore({
        key: "id",
        loadMode: "raw",
        load: () => fakeData(),
      });
    }

    function fakeData(): Promise<any[]> {
      return new Promise((resolve) => {
        const items = [];
        for (let i = 0; i < 1000; i++) {
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
      componentKey,
      dataSource,
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
    <button :disabled="isLoading" @click="getData">Re-fetch Data</button>
    <DataTable v-if="dataSource" :data-source="dataSource" />
  </div>
</template>
