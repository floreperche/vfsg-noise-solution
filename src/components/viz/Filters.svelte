<script>
  import RangeSlider from "svelte-range-slider-pips";
  import OriginFilter from "./OriginFilter.svelte";
  export let selectedOrigin;
  export let minAge;
  export let maxAge;

  // Age filter
  let values = [minAge, maxAge];
  $: {
    minAge = values[0];
    maxAge = values[1];
  }
</script>

<div class="filter-container">
  <h2>Filter the results</h2>
  <div style="display:flex; justify-content: space-between" class="filters">
    <div
      style="display:flex; flex-direction:column; justify-content: space-between"
    >
      <div style="display:flex; justify-content: space-around">
        <!-- Age filter -->
        <div class="age" style="width: 200px">
          <p class="title">age</p>
          <div>
            <RangeSlider range min={4} max={60} bind:values float />
          </div>
        </div>
        <div class="location">
          <p class="title">location</p>
          <div></div>
        </div>
      </div>
      <div class="gender">
        <p class="title">gender</p>
        <div></div>
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
    border: 1px solid black;
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
    width: 170px;
  }
</style>
