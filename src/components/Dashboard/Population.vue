<template>
  <div class="population">
    <div class="section">
      <span class="section--label">Population</span>
      <span class="section--count--value">{{
        localityPopulation["attributes"] &&
        localityPopulation["attributes"]["population"]
          ? localityPopulation["attributes"]["population"]
          : "NA"
      }}</span>
    </div>
    <div class="section">
      <span class="section--label">Households</span
      ><span class="section--households--value">{{ localityPopulation && localityPopulation["attributes"]
        ? localityPopulation["attributes"]["households"]
        : "NA" }}</span>
    </div>
    <div class="section">
      <span class="section--label">{{localityPopulation && localityPopulation["attributes"]
        && localityPopulation["attributes"]["pincode"]?'Pincode':'Locality'}}</span
      ><span class="section--country--value">{{ localityPopulation && localityPopulation["attributes"]
        ? localityPopulation["attributes"]["pincode"] || localityPopulation["attributes"]["locality"]
        : "NA"}}</span>
    </div>
    <div class="section">
      <span class="section--label">District</span
      ><span class="section--district--value">{{ localityPopulation && localityPopulation["attributes"]
        ? localityPopulation["attributes"]["city"] || localityPopulation["attributes"]["district_n"]
        : "NA"}}</span>
    </div>
    
  </div>
</template>

<script>
export default {
  name: "Population",
  props: ["population"],
  computed: {
    localityPopulation() {
      return { ...this.population };
    }
  }
};
</script>

<style lang="scss" scoped>
.population {
  background-color: $color-white;
  grid-area: $grid-population;
    @include display-container(grid,center);
   justify-items: stretch;
  grid-template-columns: 1fr 1fr;
  grid-gap: .2rem;
  color: $color-white;
 
  .section {
    @include display-container(flex,center);
    @include flex-direction(column);
    justify-content: center;
    font-size: 2rem;
    padding: 20px;
    height: 100%;
    background-color: $color-primary;

    &--label {
      color: black;
      padding: 1rem;
    }
  }
}
</style>
