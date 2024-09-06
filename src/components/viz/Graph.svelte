<script>
  export let xScale;
  export let yScale;
  export let radiusScale;
  export let result;
  export let chartWidth;
  export let chartHeight;
  export let xTicks;
  export let yTicks;
</script>

<div class="chart-container">
  <div class="chart">
    <svg height={chartHeight} width={chartWidth}>
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
          <g transform="translate({xScale(7.4)}, {yScale(23.5)})" opacity="0.8">
            <text
              x="0"
              y="0"
              dominant-baseline="middle"
              fill="white"
              font-size="14">Low initial well-being,</text
            ><text
              x="0"
              y="15"
              dominant-baseline="middle"
              fill="white"
              font-size="14">improved after mentorship</text
            ></g
          >
          <g
            transform="translate({xScale(34.6)}, {yScale(23.5)})"
            opacity="0.8"
          >
            <text
              x="0"
              y="0"
              dominant-baseline="middle"
              text-anchor="end"
              fill="white"
              font-size="14">High initial well-being,</text
            ><text
              x="0"
              y="15"
              dominant-baseline="middle"
              text-anchor="end"
              fill="white"
              font-size="14">improved after mentorship</text
            ></g
          >

          <g
            transform="translate({xScale(7.4)}, {yScale(-13.5)})"
            opacity="0.8"
          >
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
              font-size="14">deteriorated after mentorship</text
            ></g
          >
          <g
            transform="translate({xScale(34.6)}, {yScale(-13.5)})"
            opacity="0.8"
          >
            <text
              x="0"
              y="-15"
              dominant-baseline="middle"
              text-anchor="end"
              fill="white"
              font-size="14">High initial well being,</text
            ><text
              x="0"
              y="0"
              dominant-baseline="middle"
              text-anchor="end"
              fill="white"
              font-size="14">deteriorated after mentorship</text
            ></g
          >

          <!-- Chart circles -->
          {#each result as node, i}
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

<style>
  .chart {
    width: fit-content;
    height: fit-content;
    padding: 20px 14px;
    margin-top: 50px;
    background-color: #02070b;
    border-radius: 10px;
  }
</style>
