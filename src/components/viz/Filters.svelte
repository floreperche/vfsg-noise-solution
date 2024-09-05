<script></script>

<div class="filter-container">
  <h2>Filter the results</h2>
  <div style="display:flex; justify-content: space-between" class="filters">
    <div
      style="display:flex; flex-direction:column; justify-content: space-between"
    >
      <div style="display:flex; justify-content: space-around">
        <div class="age">
          <p class="title">age</p>
          <div></div>
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
      <div></div>
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

  .filter-container .age,
  .filter-container .location,
  .filter-container .gender,
  .filter-container .origin {
    border: 1px solid white;
  }

  .filter-container .gender {
    width: 380px;
  }

  .filter-container .origin {
    width: 10px;
  }
</style>
