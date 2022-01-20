<script>
import { onBeforeMount, onMounted, ref } from "vue";
import HeaderVue from "./components/Header.vue";
import WaybillDataViewVue from "./components/WaybillDataView.vue";
import LoadingStateVue from "./components/LoadingState.vue";
export default {
  components: {
    HeaderVue,
    WaybillDataViewVue,
    LoadingStateVue
  },
  setup() {
    const waybillData = ref({});
    const isLoading = ref(false);

    async function getWaybillData() {
      isLoading.value = true;
      const response = await fetch("https://mocki.io/v1/de8e9ad3-bd34-445e-87b3-c44e6e3efbe9");
      const data = await response.json();
      if (data) {
        waybillData.value = data;
      }
      isLoading.value = false;
    }

    onMounted(async () => await getWaybillData());

    return { waybillData, isLoading };
  },
};
</script>

<template>
  <div id="app">
    <header-vue />
    <waybill-data-view-vue
      v-if="!isLoading"
      :data="waybillData" />
    <loading-state-vue v-else />
  </div>
</template>

<style></style>
