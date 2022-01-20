<template>
  <div class="columns ml-4">
    <div class="column is-narrow">
      <p class="is-size-7">Equipment ID</p>
      <p class="is-size-7">{{ data.asset?.equipment_id  }}</p>
    </div>
    <div class="column is-narrow">
      <p class="is-size-7">Created</p>
      <p class="is-size-7">{{ formattedCreatedDate }}</p>
    </div>
    <div class="column is-narrow">
      <p class="is-size-7">Origin</p>
      <p class="is-size-7">{{ data.asset?.origin_location }}</p>
    </div>
    <div class="column is-narrow">
      <p class="is-size-7">Destination</p>
      <p class="is-size-7">{{ data.asset?.destination_location }}</p>
    </div>
    <div class="column is-narrow">
      <p class="is-size-7">Status</p>
      <p class="is-size-7">{{ data.asset?.status }}</p>
    </div>
    <div class="column is-narrow">
      <p class="is-size-7">ETA</p>
      <p class="is-size-7">{{ formattedEtaDate }}</p>
    </div>
  </div>
</template>

<script>
import dayJs from "dayjs";
export default {
  props: {
    data: {
      type: Object,
      default: () => {}
    }
  },
  computed: {
    formattedCreatedDate() {
      return dayJs(this.data.waybill?.created_date).format("MM/DD/YYYY");
    },
    formattedEtaDate() {
      return dayJs(this.data.waybill?.eta_date).format("MM/DD/YYYY");
    }
  }
}
</script>