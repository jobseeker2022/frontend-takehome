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
    <map-vue :waypoints="data.milestones"/>
  </div>
</template>

<script>
import dayJs from "dayjs";
import MapVue from "./Map.vue";
export default {
  components: { MapVue },
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