<template>
  <nav class="navbar">
    <h1 class="navbar--heading">Web Reports</h1>
    <div class="navbar--input">
      <form @submit.prevent="SearchData" class="navbar--input--form">
        <div class="radio-select">
          <label for="one">Locality</label
          ><input
            type="radio"
            id="one"
            value="true"
            v-model="form.serachByLocality"
          />
          <label for="two">Pincode</label>

          <input
            type="radio"
            id="two"
            value="false"
            v-model="form.serachByLocality"
          />
        </div>
        <div class="searchBar">
          <input
            :type="form.serachByLocality == 'true' ? 'text' : 'number'"
            class="navbar--input__text"
            :placeholder="
              form.serachByLocality == 'true'
                ? 'Search By Locality'
                : 'Search By Pincode'
            "
            v-model="form.searchInput"
            required
          />
          <span v-if="form.serachByLocality == 'false'" class="searchBar--text">
            *Must be valid 6 digits(eg: 560040)</span
          >
          <span v-else class="searchBar--text">
            *Must be valid (eg: kaveri nagar)</span
          >
        </div>
        <input class="navbar--input__button" type="submit" value="Search" />
      </form>
    </div>
  </nav>
</template>

<script>
export default {
  name: "NavbarSearch",
  data() {
    return {
      form: {
        searchInput: "",
        serachByLocality: "true"
      }
    };
  },
  methods: {
    SearchData() {
      if (this.form.searchInput) {
       if(this.form.serachByLocality=='false'
         && this.form.searchInput.length<6){
            return;
         }
        else{
        // console.log(this.form.searchInput);
        this.$emit("searchInput", this.form);
        this.form.searchInput = "";
      }
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.navbar {
  background-color: #1e90ff;
  grid-area: $grid-navbar;
  padding: 10px;
  @include display-container(grid, center);
  grid-template-columns: 1fr 1fr;
  @media only screen and (max-width: 700px) {
    grid-template-columns: 1fr;
  }
  &--heading {
    @include justify-align-self(center, center);
    font-size: 3rem;
    color: $color-white;
  }
  &--input {
    display: flex;
    justify-content: start;
    align-self: stretch;
    @media only screen and (max-width: 700px) {
      justify-content: center;
    }
    &--form {
      @include display-container(flex, center);
      @media only screen and (max-width: 700px) {
        @include flex-direction(column);
      }
      .searchBar {
        flex-direction: column;
        display: flex;
        align-self: stretch;
        margin-top: 2.5rem;
        justify-content: center;
        @media only screen and (max-width: 700px) {
          margin-top: 0;
        }

        &--text {
          color: white;

          font-size: 1.2rem;
          padding: 5px;
          @media only screen and (max-width: 700px) {
            letter-spacing: 2px;
            margin-bottom: 1rem;
          }
        }
      }
      .radio-select {
        @include display-container(flex, center);

        margin-right: 1rem;
        padding: 1rem;
        label {
          font-size: 2rem;
          padding: 1rem;
        }
      }
    }
    &__checkbox {
      margin-right: 1rem;
      padding: 1rem;
    }

    &__text {
      margin-right: 1rem;
      border: none;
      border-radius: 5px;
      padding: 1rem;
      @media only screen and (max-width: 700px) {
        margin-bottom: 1rem;
      }
    }
    &__button {
      background-color: #4caf50; /* Green */
      border: none;
      border-radius: 5px;
      color: white;
      padding: 1rem;
      text-align: center;
      text-decoration: none;
      display: inline-block;
      font-size: 1.6rem;
    }
  }
}
</style>
