<script>
  import RangeSlider from "svelte-range-slider-pips";
  export let minAge;
  export let maxAge;

  let values = [minAge, maxAge];
  $: {
    minAge = values[0];
    maxAge = values[1];
  }
</script>

<div>
  <RangeSlider range min={4} max={60} bind:values float />
</div>
