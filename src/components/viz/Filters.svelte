<script>
  import RangeSlider from "svelte-range-slider-pips";
  import OriginFilter from "./OriginFilter.svelte";
  import GenderFilter from "./GenderFilter.svelte";
  import LocationFilter from "./LocationFilter.svelte";
  export let selectedOrigin;
  export let minAge;
  export let maxAge;
  export let genderValues;
  export let selectedLocation;

  // Age filter
  let values = [minAge, maxAge];
  $: {
    minAge = values[0];
    maxAge = values[1];
  }
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
          <div>
            <RangeSlider range min={4} max={60} bind:values float />
          </div>
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

  .filter-container .title {
    text-transform: uppercase;
  }

  .filter-container .age {
    --range-slider: #d5d5d5;
    --range-handle-inactive: #eeeeee;
    --range-handle-focus: #eeeeee;
    --range-handle: #eeeeee;
    --range-range: #ffb997;
    --range-range-inactive: #ffb997;
    --range-float-inactive: #313131;
    --range-float: #313131;
    --range-float-text: white;
  }

  .filter-container .gender {
    width: 380px;
  }

  .filter-container .origin {
    width: 165px;
  }
</style>
