<script lang="ts">
import { defineComponent, watch, ref, computed } from "vue";
import { DxDataGrid } from "devextreme-vue/data-grid";

export default defineComponent({
  components: {
    DxDataGrid,
  },
  props: {
    items: {
      type: Array,
      default: null,
    },
  },
  setup(props: { items: Array<any> }) {
    const gridRef = ref(null);
    const gridData = ref<any[]>();
    const gridColumns = computed(() => {
      const columns = [
        {
          dataField: "id",
          dataType: "number",
        },
        {
          dataField: "name",
          dataType: "string",
        },
      ];

      const alpha = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
      for (const letter in alpha) {
        let dataType;
        if (["A", "B", "C"].includes(alpha[letter])) {
          dataType = "string";
        } else {
          dataType = "number";
        }
        columns.push({
          dataField: alpha[letter],
          dataType,
        });
      }
      return columns;
    });

    function loadData() {
      if (!props.items) return;
      gridData.value = props.items;
    }

    watch(
      () => props.items,
      () => {
        if (!props.items) return;
        gridData.value = props.items;
      }
    );

    loadData();

    return {
      gridData,
      gridRef,
      gridColumns,
    };
  },
});
</script>
<template>
  <DxDataGrid
    v-show="gridData"
    width="1000"
    height="800"
    ref="gridRef"
    :column-auto-width="true"
    :data-source="gridData"
    :columns="gridColumns"
  />
</template>
