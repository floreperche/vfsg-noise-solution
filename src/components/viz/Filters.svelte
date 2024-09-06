<script>
  import OriginFilter from "./OriginFilter.svelte";
  import GenderFilter from "./GenderFilter.svelte";
  import LocationFilter from "./LocationFilter.svelte";
  import AgeFilter from "./AgeFilter.svelte";
  export let selectedOrigin;
  export let minAge;
  export let maxAge;
  export let genderValues;
  export let selectedLocation;

  // Age filter
</script>

<div class="filter-container">
  <h2>Filter the results</h2>
  <div
    style="display:flex; justify-content: space-between; gap:30px "
    class="filters"
  >
    <div
      style="display:flex; flex-direction:column; justify-content: space-between"
    >
      <div style="display:flex;  gap:30px; ">
        <!-- Age filter -->
        <div class="age" style="width: 180px">
          <p class="title">age</p>
          <AgeFilter bind:minAge bind:maxAge />
        </div>
        <div class="location">
          <p class="title">location</p>
          <LocationFilter bind:selectedLocation />
        </div>
      </div>
      <div class="gender">
        <p class="title">gender</p>
        <GenderFilter bind:genderValues />
      </div>
    </div>

    <div class="origin">
      <p class="title">origin</p>
      <OriginFilter bind:selectedOrigin />
    </div>
  </div>
</div>

<style>
  .filter-container {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  .filter-container h2 {
    padding-left: 0px;
  }

  .filter-container .title {
    text-transform: uppercase;
  }

  .filter-container .age {
    --range-slider: #959595;
    --range-handle-inactive: #eeeeee;
    --range-handle-focus: #eeeeee;
    --range-handle: #eeeeee;
    --range-range: #ffb997;
    --range-range-inactive: #ffb997;
    --range-float-inactive: #313131;
    --range-float: #313131;
    --range-float-text: white;
    --range-handle-border: transparent;
  }

  .filter-container .gender {
    width: 380px;
  }

  .filter-container .origin {
    width: 165px;
  }
</style>
