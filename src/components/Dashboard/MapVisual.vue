<template>
  <div class="map">
    <div>Hellowor  nbj</div>
  </div>
</template>

<script>
// import { MglMap , MglPopUp} from "vue-mapbox";

export default {
  name: "MapVisual",
  data() {
    return {
      accessToken:
        "pk.eyJ1IjoibmlraGlsamhhIiwiYSI6ImNrOG9rd3gyNjB1Z2wzZXJ4NHg0eDU3a2gifQ.lXENFoV9AIjSAKcJN6Pb-Q", // your access token. Needed if you using Mapbox maps
      mapStyle: "mapbox://styles/mapbox/light-v9", // your map style,
      popupCoordinates: [77.488113, 13.002949]
    };
  }
  // components: {
  //   "MglMap" : MglMap,
  //   "MglPopUp": MglPopUp
  // }
};
</script>

<style>
</style>
