<template>
  <div>
    <table class="table ml-4">
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
          <td class="is-uppercase">{{ data.asset?.status }}</td>
          <td>{{ formattedEtaDate }}</td>
        </tr>
      </tbody>
    </table>
    <map-vue
      :waypoints="data.milestones"
      :center="midpoint"
    />
  </div>
</template>

<script>
import dayJs from "dayjs";
import MapVue from "./Map.vue";
import { computed } from "vue";
export default {
  components: { MapVue },
  props: {
    data: {
      type: Object,
      default: () => {}
    }
  },
  setup(props) {
    const formattedCreatedDate = computed(() => {
      return dayJs(props.data.waybill?.created_date).format("MM/DD/YYYY");
    });
    const formattedEtaDate = computed(() => {
      return dayJs(props.data.waybill?.eta_date).format("MM/DD/YYYY");
    });
    const midpoint = computed(() => {
      const originLongitude = parseFloat(props.data.waybill?.origin.longitude);
      const orginLatitude = parseFloat(props.data.waybill?.origin.latitude);
      const destinationLongitude = parseFloat(props.data.waybill?.destination.longitude);
      const destinationLatitude = parseFloat(props.data.waybill?.destination.latitude);
      return [(originLongitude + destinationLongitude) / 2, (orginLatitude + destinationLatitude) / 2];

    })
    return { formattedCreatedDate, formattedEtaDate, midpoint }
  }
}
</script>