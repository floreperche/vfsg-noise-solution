<script>
  import rawData from "../data/results.json";
  //   const arr = [
  //     { start_code: 1, end_code: 2, filter: true },
  //     { start_code: 1, end_code: 2, filter: false },
  //     { start_code: 1, end_code: 3, filter: false },
  //     { start_code: 3, end_code: 1, filter: true },
  //     { start_code: 3, end_code: 2, filter: true },
  //     { start_code: 3, end_code: 2, filter: true },
  //   ];

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
        result.find(
          (el) => el.start === ele.start_code && el.gap === ele.end_code
        )
      ) {
        let index = result.findIndex(
          (el) => el.start === ele.start_code && el.gap === ele.end_code
        );
        result[index].count += 1;
      } else {
        result.push({
          start: ele.start_code,
          gap: ele.end_code,
          count: 1,
        });
      }
    });
  }

  $: console.log("result", result);
</script>

<div class="viz-container">
  <div class="graph-container">
    <div class="graph"></div>
  </div>
</div>

<style>
  .viz-container {
    height: 80vh;
    background: linear-gradient(-60deg, #2c2c2e, #585a5e);
    border-radius: 10px;
  }
</style>
