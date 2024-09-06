<script>
  import RangeSlider from "svelte-range-slider-pips";
  export let selectedOrigin;
  let values = [0];
  const originValues = [
    { id: 0, value: "all", code: "all" },
    { id: 1, value: "education", code: "education" },
    { id: 2, value: "local govern.", code: "local_gov" },
    { id: 3, value: "mental health", code: "mental_health" },
    { id: 4, value: "other", code: "other" },
  ];
  $: {
    selectedOrigin = originValues[values[0]];
  }
</script>

<div class="origin-filter" style="position: relative">
  <RangeSlider vertical step={1} max={4} pips bind:values reversed />
  <div class="label">
    {#each originValues as label}
      {#if label.id === values[0]}
        <p style="font-weight: 700">{label.value}</p>{:else}<p
          style="opacity: 0.6"
        >
          {label.value}
        </p>{/if}
    {/each}
  </div>
</div>

<style>
  .origin-filter {
    --range-slider: #d5d5d5;
    --range-handle-inactive: #ffb997;
    --range-handle-focus: #ffb997;
    --range-handle: #ffb997;
    --range-range: #ffb997;
    --range-range-inactive: #ffb997;
    --range-pip-in-range: white;
    --range-pip-active: white;
    --range-handle-border: transparent;
  }

  .label {
    position: absolute;
    top: 0;
    left: 44px;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding-top: 4px;
    padding-bottom: 2px;
  }
</style>
