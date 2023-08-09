<script lang="ts">
import { defineComponent, ref, computed } from "vue";
import type { PropType } from "vue";
import { DxTreeList, DxScrolling, DxSorting } from "devextreme-vue/tree-list";
import type CustomStore from "devextreme/data/custom_store";

export default defineComponent({
  components: {
    DxTreeList,
    DxScrolling,
    DxSorting,
  },
  props: {
    dataSource: {
      type: Object as PropType<CustomStore>,
      required: true,
    },
  },
  setup(props: any) {
    const gridRef = ref(null);
    let treeListInstance: any = null;
    const gridColumns = computed(() => {
      const columns = [
        {
          dataField: "name",
          dataType: "string",
        },
      ];

      const alpha = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
      for (const letter in alpha as any) {
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

    function saveTreeListInstance(e: any) {
      treeListInstance = e.component;
    }

    return {
      gridRef,
      gridColumns,
      saveTreeListInstance,
    };
  },
});
</script>
<template>
  <DxTreeList
    v-show="dataSource"
    width="1000"
    height="800"
    ref="gridRef"
    :column-auto-width="true"
    :data-source="dataSource"
    :columns="gridColumns"
    :scrolling="{ mode: 'standard' }"
    key-expr="id"
    data-structure="plain"
    @initialized="saveTreeListInstance"
  >
    <dx-sorting mode="multiple" />
    <dx-scrolling :use-native="false" show-scrollbar="always" />
  </DxTreeList>
</template>
