<template>
  <div id="map" class="m-auto mt-4"></div>
</template>

<script>
import mapboxgl from "mapbox-gl";
import { onMounted, computed } from "vue";
export default {
  props: {
    waypoints: {
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

    function createMap() {
      try {
        mapboxgl.accessToken = accessToken;
        const map = new mapboxgl.Map({
          container: "map",
          style: "mapbox://styles/mapbox/streets-v11",
          center: center,
          zoom: 4,
        });

      } catch (err) {
        console.log("map error", err);
      }
    }

    onMounted(() => createMap());
    return { };
  }
}
</script>

<style scoped>
  #map {
    height: 50vh;
    width: 80vw;
  }
</style>