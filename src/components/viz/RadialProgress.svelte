<script>
  import { arc, scaleLinear } from "d3";
  export let positiveImpactAverage;

  let averageValue = 20;

  const progressBackground = arc()
    .innerRadius(70)
    .outerRadius(80)
    .startAngle(-Math.PI / 1.5)
    .endAngle(Math.PI / 1.5)
    .cornerRadius(18);

  $: progressScale = scaleLinear()
    .domain([0, 100])
    .range([-Math.PI / 1.5, Math.PI / 1.5]);

  const progress = arc()
    .innerRadius(70)
    .outerRadius(80)
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
  <svg width="200" height="150">
    <g transform="translate(100,90)"
      ><path fill="#D5D5D5" d={progressBackground()} />
      <path fill="#BDFF00" d={progress(positiveImpactAverage)} />
      <circle cx="0" cy="0" r="50" fill="#373737" />
      <circle cx="0" cy="0" r="35" fill="#555555" />
      <path fill="#BDFF00" d={bubble(positiveImpactAverage)} />
    </g>
  </svg>
  <div class="comment">
    <div class="progress">
      <p class="value">{positiveImpactAverage}%</p>
      <p>of the selected participants</p>
    </div>
    <div>improved their wellbeing with Noise Solution.</div>
  </div>
</div>

<style>
  .radial-progress {
    width: 300px;
    height: fit-content;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
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
    font-size: 44px;
    color: #bdff00;
    text-align: left;
  }
</style>
