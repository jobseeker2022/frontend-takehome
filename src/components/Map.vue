<template>
  <div id="map" class="mt-4"></div>
</template>

<script>
import mapboxgl from "mapbox-gl";
import { onMounted, computed, ref } from "vue";
export default {
  props: {
    milestones: {
      type: Object,
      default: () => {}
    },
    center: {
      type: Array,
      default: () => [-105.00693395733833, 39.75764080440982]
    }
  },
  setup(props) {
    const accessToken = import.meta.env.VITE_MAPBOX_API_TOKEN;
    const center = props.center;
    const map = ref({});

    function addMarkers() {
      locationsToPlot.value.forEach(location => {
        new mapboxgl.Marker({
          color: "#54ADDF"
        })
        .setLngLat(location)
        .addTo(map.value);
      })
    }

    const locationsToPlot = computed(() => {
      return props.milestones?.reduce((acc, currVal) => {
        let event = currVal.events.find(event => {
          return event.location.longitude && event.location.latitude;
        });
        acc.push([parseFloat(event.location.longitude), parseFloat(event.location.latitude)]);
        return acc;
      }, [])
    })

    onMounted(() => {
        mapboxgl.accessToken = accessToken;
        map.value = new mapboxgl.Map({
          container: "map",
          style: "mapbox://styles/mapbox/streets-v11",
          center: center,
          zoom: 4,
        });
        addMarkers();
    });
    return {};
  }
}
</script>

<style scoped>
  #map {
    height: 50vh;
    width: 100%;
  }
</style>