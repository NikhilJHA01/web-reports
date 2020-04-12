<template>
  <div class="dashboard">
    <NavbarSearch @searchInput="searchInput($event)"></NavbarSearch>
    <Population :population="localityData"></Population>
    <!-- <MapVisual></MapVisual> -->
    <Income :income="incomeData"></Income>
    <Expenditure :expenditures="expenditureData"></Expenditure>
  </div>
</template>

<script>
import axios from "axios";
import Expenditure from "../components/Dashboard/Expenditure";
import Income from "../components/Dashboard/Income";
import MapVisual from "../components/Dashboard/MapVisual";
import Population from "../components/Dashboard/Population";
import NavbarSearch from "../components/Dashboard/NavbarSearch";

export default {
  name: "Dashboard",
  data() {
    return {
      serviceURL:"https://webreports-ad4e0.firebaseio.com/.json",
      expenditure: [],
      expenditureData: {},
      locality: [],
      localityData: {},
      pincode: [],
      pincodeData: {},
      income: [],
      incomeData: {}
    };
  },
  components: { Population, Income, Expenditure, MapVisual, NavbarSearch },
  created() {
    axios
      .get(this.serviceURL)
      .then(res => {
        if (res.data) {
          // console.log(res.data);
          this.locality = res.data.locality ? res.data.locality.features : [];
          this.pincode = res.data.pincode ? res.data.pincode.features : [];
          this.expenditure = res.data.expenditure ? res.data.expenditure : [];
          this.income = res.data.income ? res.data.income : [];
          // console.log(this.income);
          // console.log(this.locality.find(el => el.attributes.locality === "Andrahalli"));
          // console.log(this.locality);
        }
      })
      .catch(err => console.log(err));
  },
  methods: {
    searchInput(searchForm) {
      let searchField = searchForm.searchInput.trim().toLowerCase();
      if (
        searchForm.serachByLocality == "true" &&
        typeof searchField == "string"
      ) {
        this.searchByLocality(searchField);
      } else {
        this.searchByPincode(searchField);
      }
    },
    searchByLocality(searchField) {
      this.localityData = this.locality.find(
        el => el.attributes.locality.toLowerCase() === searchField
      );
      if (this.localityData) {
        this.incomeData = this.income.find(
          ({ locality }) =>
            locality.toLowerCase() ===
            this.localityData["attributes"]["locality"].toLowerCase()
        );
        this.expenditureData = {};
      } else {
        this.incomeData = {};
      }
      // console.log(this.incomeData);
    },
    searchByPincode(searchField) {
      this.localityData = this.pincode.find(
        el => el.attributes.pincode == searchField
      );
      if (this.localityData) {
        this.incomeData = this.pincode.find(
          pincode =>
            pincode["pincode"] == this.localityData["attributes"]["pincode"]
        );
        const expenseData = this.expenditure.find(
          ({ pincode }) => pincode == this.localityData["attributes"]["pincode"]
        );
        // this.expenditureDataN ? delete this.expenditureData["pincode"] : "";
        this.expenditureData = Object.keys(expenseData).reduce(
          (object, key) => {
            if (key !== "pincode") {
              object[key] = expenseData[key];
            }
            return object;
          },
          {}
        );
        // console.log(this.expenditureData);
      } else {
        this.incomeData = {};
        this.expenditureData = {};
      }
      // console.log(this.incomeData);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.dashboard {
  height: 95vh;
  display: grid;
  grid-gap: 1rem;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 10rem 1fr 1fr;
  grid-template-areas:
    "navbar navbar"
    "population income"
    "expenditure expenditure";

  @media only screen and (max-width: 700px) {
    grid-template-columns: auto;
    grid-template-rows: minmax(min-content, max-content) 1fr 1fr 1fr;
    grid-template-areas:
      "navbar"
      "population"
      "income"
      "expenditure";
  }
}
</style>
