<template>
  <div id="map" class="ml-4"></div>
</template>

<script>
import mapboxgl from "mapbox-gl";
import { onMounted, ref } from "vue";
export default {
  props: {
    waypoints: {
      type: Object
    }
  },
  setup(props) {
    const accessToken = import.meta.env.VITE_MAPBOX_API_TOKEN;
    const center = [-84.564397, 35.5];

    async function createMap() {
      try {
        mapboxgl.accessToken = accessToken;
        const map = await new mapboxgl.Map({
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
    width: 50vw;
  }
</style>