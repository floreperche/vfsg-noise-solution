<script>
  import rawData from "../data/results.json";
  import { scaleLinear, scaleSqrt } from "d3";

  //   Filter data
  let filter = false;
  let filteredData = [...rawData];

  //   $: {
  //     filteredData = [];
  //     if (filter) {
  //       rawData.map((el) => {
  //         if (el.filter) {
  //           //   console.log(el);
  //           filteredData.push(el);
  //         }
  //       });
  //     } else {
  //       filteredData = [...arr];
  //     }
  //   }

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

  // $: console.log(result);

  // Chart
  $: chartWidth = 820;
  $: chartHeight = 400;

  $: xScale = scaleLinear().domain([6.5, 35.5]).range([0, chartWidth]);
  $: yScale = scaleLinear().domain([-15.5, 25.5]).range([chartHeight, 0]);
  $: radiusScale = scaleSqrt().domain([1, 9]).range([2, 8]);

  $: xTicks = [7, 9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 29, 31, 33, 35];
  $: yTicks = [-15, -10, -5, 0, 5, 10, 15, 20, 25];

  $: console.log(xTicks);
</script>

<div class="viz-container">
  <div class="chart-container">
    <div class="chart">
      <svg width={chartWidth} height={chartHeight}>
        <g
          >{#if result}
            <!-- Grid -->
            {#each xTicks as xTick}
              <g transform="translate({xScale(xTick)}, 0)"
                ><line
                  x1="0"
                  x2="0"
                  y1={yScale(-15)}
                  y2={yScale(25)}
                  stroke="white"
                  opacity={xTick === 21 ? "1" : "0.2"}
                />

                <line
                  x1="0"
                  x2="0"
                  y1={yScale(-0.5)}
                  y2={yScale(0.5)}
                  stroke="white"
                  opacity="0.8"
                />
                <text
                  x="0"
                  y={yScale(-2)}
                  text-anchor="middle"
                  opacity="0.8"
                  fill="white"
                  font-size="12">{xTick}</text
                ></g
              >
            {/each}
            {#each yTicks as yTick}
              <g transform="translate(0, {yScale(yTick)})">
                <line
                  x1={xScale(7)}
                  x2={xScale(35)}
                  y1="0"
                  y2="0"
                  stroke="white"
                  opacity={yTick === 0 ? "1" : "0.2"}
                />
                <line
                  x1={xScale(20.8)}
                  x2={xScale(21.2)}
                  y1="0"
                  y2="0"
                  stroke="white"
                  opacity="0.8"
                />
                <text
                  x={xScale(21.5)}
                  y="0.5"
                  dominant-baseline="middle"
                  fill="white"
                  opacity="0.8"
                  font-size="12"
                  >{#if yTick > 0}
                    + {yTick}{:else}{yTick}{/if}</text
                ></g
              >
            {/each}
            <!-- Comments -->
            <g transform="translate({xScale(7.2)}, {yScale(24)})">
              <text
                x="0"
                y="0"
                dominant-baseline="middle"
                fill="white"
                font-size="14">Low initial well being,</text
              ><text
                x="0"
                y="15"
                dominant-baseline="middle"
                fill="white"
                font-size="14">improved after mentorship</text
              ></g
            >
            <g transform="translate({xScale(34.8)}, {yScale(24)})">
              <text
                x="0"
                y="0"
                dominant-baseline="middle"
                text-anchor="end"
                fill="white"
                font-size="14">Low initial well being,</text
              ><text
                x="0"
                y="15"
                dominant-baseline="middle"
                text-anchor="end"
                fill="white"
                font-size="14">improved after mentorship</text
              ></g
            >

            <g transform="translate({xScale(7.2)}, {yScale(-14)})">
              <text
                x="0"
                y="-15"
                dominant-baseline="middle"
                fill="white"
                font-size="14">Low initial well being,</text
              ><text
                x="0"
                y="0"
                dominant-baseline="middle"
                fill="white"
                font-size="14">improved after mentorship</text
              ></g
            >
            <g transform="translate({xScale(34.8)}, {yScale(-14)})">
              <text
                x="0"
                y="-15"
                dominant-baseline="middle"
                text-anchor="end"
                fill="white"
                font-size="14">Low initial well being,</text
              ><text
                x="0"
                y="0"
                dominant-baseline="middle"
                text-anchor="end"
                fill="white"
                font-size="14">improved after mentorship</text
              ></g
            >

            <!-- Chart circles -->
            {#each result as node}
              <circle
                cx={xScale(node.start)}
                cy={yScale(node.gap)}
                r={radiusScale(node.count)}
                fill={node.gap > 0
                  ? "#BDFF00"
                  : node.gap < 0
                    ? "#8655FF"
                    : "#FFFFFF"}
              />
            {/each}{/if}
        </g>
      </svg>
    </div>
  </div>
</div>

<style>
  .viz-container {
    height: 80vh;
    background: linear-gradient(-60deg, #2c2c2e, #585a5e);
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .viz-container .chart {
    width: fit-content;
    height: fit-content;
    padding: 40px;

    margin-top: 50px;
    background-color: #02070b;
    border-radius: 10px;
  }
</style>
