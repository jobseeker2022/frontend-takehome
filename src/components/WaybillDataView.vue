<template>
  <div class="waybill-data-container">
    <table class="table is-fullwidth">
      <thead>
        <tr>
          <th>Equipment ID</th>
          <th>Created</th>
          <th>Origin</th>
          <th>Destination</th>
          <th>Status</th>
          <th>ETA</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>{{ data.asset?.equipment_id  }}</td>
          <td>{{ formattedCreatedDate }}</td>
          <td>{{ data.asset?.origin_location }}</td>
          <td>{{ data.asset?.destination_location }}</td>
          <td class="is-uppercase" :class="{'red': data.asset?.status !== 'Complete'}">{{ data.asset?.status }}</td>
          <td  :class="{'red': isWaybillLate }">{{ formattedEtaDate }}</td>
        </tr>
      </tbody>
    </table>
    <map-vue
      v-if="data.milestones"
      :milestones="data.milestones"
      :center="center"
    />
    <div class="mt-6">
      <a class="is-size-4 is-underlined" @click="showEventsModal = true">View Events</a>
    </div>
    <events-modal-vue
      v-if="showEventsModal"
      :show-events-modal="showEventsModal"
      :events="data.events"
      @close="showEventsModal = false"
      />
  </div>
</template>

<script>
import dayJs from "dayjs";
import MapVue from "./Map.vue";
import EventsModalVue from "./EventsModal.vue";
import { computed, ref } from "vue";
export default {
  components: {
    MapVue,
    EventsModalVue
  },
  props: {
    data: {
      type: Object,
      default: () => {}
    }
  },
  setup(props) {
    const showEventsModal = ref(false);
    const formattedCreatedDate = computed(() => {
      return dayJs(props.data.waybill?.created_date).format("MM/DD/YYYY");
    });
    const formattedEtaDate = computed(() => {
      return dayJs(props.data.asset?.eta_date).format("MM/DD/YYYY");
    });
    const center = computed(() => {
      const originLongitude = Number(props.data.waybill?.origin.longitude);
      const orginLatitude = Number(props.data.waybill?.origin.latitude);
      const destinationLongitude = Number(props.data.waybill?.destination.longitude);
      const destinationLatitude = Number(props.data.waybill?.destination.latitude);
      return [(originLongitude + destinationLongitude) / 2, (orginLatitude + destinationLatitude) / 2];
    })

    const isWaybillLate = computed(() => {
      if (formattedEtaDate > dayJs().format('MM/DD/YYYY')) {
        return true;
      }
      return false;
    })
    return { formattedCreatedDate, formattedEtaDate, center, showEventsModal, isWaybillLate }
  }
}
</script>

<style scoped>
  .waybill-data-container {
    width: 100%;
  }
  .red {
    color: maroon;
  }
</style>