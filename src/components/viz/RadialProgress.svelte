<script>
  import { arc, scaleLinear } from "d3";
  import { tweened } from "svelte/motion";
  import { cubicInOut } from "svelte/easing";
  export let positiveImpactAverage;
  export let filteredData;

  // Managing dynamic scales
  const tAverage = tweened(undefined, {
    delay: 0,
    duration: 300,
    easing: cubicInOut,
  });

  $: tAverage.set(positiveImpactAverage);

  // $: console.log($tAverage);

  const progressBackground = arc()
    .innerRadius(60)
    .outerRadius(70)
    .startAngle(-Math.PI / 1.5)
    .endAngle(Math.PI / 1.5)
    .cornerRadius(18);

  $: progressScale = scaleLinear()
    .domain([0, 100])
    .range([-Math.PI / 1.5, Math.PI / 1.5]);

  const progress = arc()
    .innerRadius(60)
    .outerRadius(70)
    .startAngle(-Math.PI / 1.5)
    .endAngle((d) => progressScale(d))
    .cornerRadius(18);

  const bubble = arc()
    .innerRadius(19)
    .outerRadius(25)
    .startAngle((d) => progressScale(d - 3))
    .endAngle((d) => progressScale(d + 3))
    .cornerRadius(18);

  //   console.log(progress);
</script>

<div class="radial-progress">
  {#if filteredData[0]}
    <svg width="200" height="140">
      <defs>
        <!-- Effects -->

        <filter id="inset-shadow">
          <feColorMatrix
            in="SourceGraphic"
            type="matrix"
            values="0 0 0 0 0 
            0 0 0 0 0 
            0 0 0 0 0 
            0 0 0 100 0"
            result="opaque-source"
          />
          <feGaussianBlur stdDeviation="5" />
          <feOffset dy="5" />
          <feComposite operator="xor" in2="opaque-source" />
          <feComposite operator="in" in2="opaque-source" />
          <feComposite operator="over" in2="SourceGraphic" />
        </filter>
      </defs>

      <!-- SVG -->
      <g transform="translate(100,80)"
        ><path fill="#959595" d={progressBackground()} />
        <path fill="#BDFF00" d={progress($tAverage)} class="highlight" />

        <circle
          cx="0"
          cy="0"
          r="47"
          fill="#373737"
          filter="url(#inset-shadow)"
        />
        <circle cx="0" cy="0" r="32" class="inner-circle" />
        <path fill="#BDFF00" d={bubble($tAverage)} />
      </g>
    </svg>
    <div class="comment">
      <div class="progress">
        <p class="value">{Math.round($tAverage)}%</p>
        <p>of the {filteredData.length} selected</p>
      </div>
      <div>participants improved their wellbeing with Noise Solution.</div>
    </div>{:else}
    <div
      class="comment"
      style="display:flex; flex-direction:column; justify-content:center; gap:20px; height:100%"
    >
      <div class="progress">
        <p class="value">Oops</p>
      </div>
      <div>
        There is not participant corresponding to this or these filter(s).
      </div>
    </div>
  {/if}
</div>

<style>
  .radial-progress {
    width: 260px;
    height: 240px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .radial-progress svg {
    margin-right: 20px;
  }

  .radial-progress .comment {
    display: flex;
    flex-direction: column;
  }

  .radial-progress .comment .progress {
    display: flex;
    align-items: center;
  }

  .radial-progress .comment .progress p {
    flex: 1;
  }

  .radial-progress .comment .progress .value {
    font-family: "Dela Gothic One", sans-serif;
    font-weight: 400;
    font-style: normal;
    line-height: 100%;
    font-size: 40px;
    color: #bdff00;
    text-align: left;
  }

  .radial-progress .highlight {
    -webkit-filter: drop-shadow(0px 0px 3px #bdff00);
    filter: drop-shadow(0px 0px 3px #bdff00);
  }

  .radial-progress .inner-circle {
    fill: #555555;
    -webkit-filter: drop-shadow(5px 5px 10px black);
    filter: drop-shadow(5px 5px 10px black);
  }
</style>
