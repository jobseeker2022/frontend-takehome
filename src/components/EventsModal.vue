<template>
  <div class="modal" :class="{'is-active': showEventsModal === true }">
    <div class="modal-background"></div>
    <div class="modal-content">
      <div class="event-container m-auto">
        <table class="table is-fullwidth">
          <thead>
            <tr>
              <th>Sighting Date</th>
              <th>Sighting Event Code Text</th>
              <th>Train Alpha Code</th>
              <th>Sighting City, State</th>
            </tr>
          </thead>
          <tbody>
            <template v-for="event in events" :key="event.id">
              <tr>
                <td>{{ formattedSightingDate }}</td>
                <td>{{ event.sighting_event_code_text }}</td>
                <td>{{ event.train_alpha_code }}</td>
                <td>{{ event.location.display_name }}</td>

              </tr>
            </template>

          </tbody>
        </table>
      </div>
    </div>
    <button class="modal-close is-large" aria-label="close" @click="$emit('close', false)"></button>
  </div>
</template>

<script>
import { computed } from "vue";
import dayJs from "dayjs";
export default {
  props: {
    showEventsModal: {
      type: Boolean,
      default: false
    },
    events: {
      type: Array,
      default: () => []
    }
  },
  setup(props) {
    const formattedSightingDate = computed(() => {
      return dayJs(props.events.sighting_date).format("MM/DD/YYYY");
    });

    return { formattedSightingDate };
  }
}
</script>

<style scoped>
  .event-container {
    background: blanchedalmond;
    height: 50vh;
  }
  .modal-content {
    width: 80vw;
  }
</style>