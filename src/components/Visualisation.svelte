<script>
  import rawData from "../data/results.json";
  import { scaleLinear, scaleSqrt } from "d3";
  import Graph from "./viz/Graph.svelte";
  import RadialProgress from "./viz/RadialProgress.svelte";
  import Filters from "./viz/Filters.svelte";

  //   Filter data
  let filter = false;
  let minAge = 4;
  let maxAge = 60;
  let selectedOrigin = { id: 0, value: "all", code: "all" };
  let selectedLocation = null;
  let genderValues = [
    { id: 0, value: "female", selected: true, code: "female" },
    { id: 1, value: "male", selected: true, code: "male" },
    { id: 2, value: "non binary", selected: true, code: "non_bin" },
    { id: 3, value: "other", selected: true, code: "other" },
    { id: 4, value: "no info.", selected: true, code: "no_info" },
  ];
  let filteredData = [...rawData];

  $: console.log(selectedLocation);

  $: {
    filteredData = [];
    rawData.map((el) => {
      // Age check
      if (typeof el.age === "number" && el.age >= minAge && el.age <= maxAge) {
        // industry check
        if (
          (selectedOrigin.id > 0 && el.industry === selectedOrigin.code) ||
          selectedOrigin.id === 0
        ) {
          genderValues.map((gender) => {
            if (gender.selected && gender.code === el.gender) {
              // Location
              if (
                selectedLocation === null ||
                (selectedLocation && selectedLocation === el.location)
              )
                filteredData.push(el);
            }
          });
        }
      }
    });
  }

  // Consolidate data
  let result = [];

  $: {
    result = [];
    filteredData.map((ele) => {
      if (
        result.find((el) => el.start === ele.start_code && el.gap === ele.gap)
      ) {
        let index = result.findIndex(
          (el) => el.start === ele.start_code && el.gap === ele.gap
        );
        result[index].count += 1;
      } else {
        result.push({
          start: ele.start_code,
          gap: ele.gap,
          count: 1,
        });
      }
    });
  }

  // Calculate average
  $: positiveImpactCount = filteredData.filter((person) => person.gap > 0);
  $: positiveImpactAverage = Math.round(
    (positiveImpactCount.length / filteredData.length) * 100
  );

  // Chart
  $: chartWidth = 820;
  $: chartHeight = 400;

  $: xScale = scaleLinear().domain([6.5, 35.5]).range([0, chartWidth]);
  $: yScale = scaleLinear().domain([-15.5, 25.5]).range([chartHeight, 0]);
  $: radiusScale = scaleSqrt().domain([1, 9]).range([2, 8]);

  $: xTicks = [7, 9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 29, 31, 33, 35];
  $: yTicks = [-15, -10, -5, 0, 5, 10, 15, 20, 25];
</script>

<div class="viz-container">
  <Graph
    {xScale}
    {yScale}
    {radiusScale}
    {result}
    {chartWidth}
    {chartHeight}
    {xTicks}
    {yTicks}
  />
  <div class="bottom">
    <RadialProgress {positiveImpactAverage} />
    <div class="separator"></div>
    <Filters
      bind:minAge
      bind:maxAge
      bind:selectedOrigin
      bind:genderValues
      bind:selectedLocation
    />
  </div>
</div>

<style>
  .viz-container {
    height: fit-content;
    background: linear-gradient(-60deg, #2c2c2e, #585a5e);
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .viz-container .bottom {
    display: flex;
    justify-content: space-between;
    width: 100%;
    margin: 50px;
    padding-left: 50px;
    padding-right: 50px;
  }

  .viz-container .bottom .separator {
    height: auto;
    width: 2px;
    background-color: white;
    border-radius: 10px;
  }
</style>
