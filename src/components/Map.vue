<template>
  <div id="map" class="m-auto mt-4"></div>
</template>

<script>
import mapboxgl from "mapbox-gl";
import { onMounted, computed, ref } from "vue";
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
    let map = {};
    function createMap() {
      try {
        mapboxgl.accessToken = accessToken;
        map = new mapboxgl.Map({
          container: "map",
          style: "mapbox://styles/mapbox/streets-v11",
          center: center,
          zoom: 4,
        });
        addMarkers();
      } catch (err) {
        console.log("map error", err);
      }
    }

    function addMarkers() {
      locationsToPlot.value.forEach(location => {
        new mapboxgl.Marker({
          color: "#54ADDF"
        })
        .setLngLat(location)
        .addTo(map);
      })
    }

    const locationsToPlot = computed(() => {
      return props.waypoints?.reduce((acc, currVal) => {
        let event = currVal.events.find(event => {
          return event.location.longitude != false;
        });
        acc.push([parseFloat(event.location.longitude), parseFloat(event.location.latitude)]);
        return acc;
      }, [])
    })


    onMounted(() => createMap());
    return { locationsToPlot };
  }
}
</script>

<style scoped>
  #map {
    height: 50vh;
    width: 80vw;
  }
</style>