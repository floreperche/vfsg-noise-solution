<script>
</script>

<div>
  <h3>Legend</h3>
  <div class="legend-components">
    <!-- Size -->
    <div class="size">
      <p>Each point represents one or several participants</p>
      <div class="size-elements">
        <div>
          <div
            style="width: 4px;
              height: 4px;
              background-color: #BDFF00;
              border-radius: 10px;
              margin-left: 6px"
          ></div>
          1 participant
        </div>
        <div>⭣</div>
        <div>
          <div
            style="  width: 16px;
            height: 16px;
            background-color: #BDFF00;
            border-radius: 10px;
            margin-left: 2px"
          ></div>
          9 participants
        </div>
      </div>
    </div>

    <!-- Position -->
    <div class="position">
      <p>Each participant is positioned based,</p>
      <div class="position-items">
        <div>
          <p class="category">horizontally,</p>
          <p class="description">
            on the well-being score at the begining of the mentorship program
          </p>
        </div>
        <div>
          <p class="category">vertically,</p>
          <p class="description">
            on the evolution (in points) between the initial and final scores
          </p>
        </div>
      </div>
    </div>

    <!-- Color -->
    <div class="color">
      <p>Each participant is colored based on the score evolution</p>
      <div class="color-elements">
        <div>
          <div
            style="  width: 12px;
            height: 12px;
            background-color: #BDFF00;
            border-radius: 10px"
          ></div>
          Score improved after mentorship
        </div>
        <div>
          <div
            style="  width: 12px;
             height: 12px;
             background-color: #FFFFFF;
             border-radius: 10px"
          ></div>
          Score unchanged after mentorship
        </div>
        <div>
          <div
            style="  width: 12px;
             height: 12px;
             background-color: #8655FF;
             border-radius: 10px"
          ></div>
          Score deteriorated after mentorship
        </div>
      </div>
    </div>
  </div>
</div>

<style>
  .legend-components {
    display: flex;
    gap: 20px;
  }

  .legend-components,
  .legend-components p {
    font-size: 16px;
  }

  .legend-components .size {
    flex: 1.5;
  }

  .legend-components .position,
  .legend-components .color {
    flex: 2;
  }

  .legend-components .size > p,
  .legend-components .position > p,
  .legend-components .color > p {
    padding-bottom: 12px;
  }

  .legend-components .size .size-elements > div {
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .legend-components .position .position-items {
    display: flex;
    flex-direction: column;
    gap: 8px;
  }

  .legend-components .position .position-items > div {
    display: flex;
  }

  .legend-components .position .position-items .category {
    font-weight: 700;
    flex: 1;
  }

  .legend-components .position .position-items .description {
    flex: 2;
  }

  .legend-components .color .color-elements {
    display: flex;
    flex-direction: column;
    gap: 4px;
  }

  .legend-components .color .color-elements > div {
    display: flex;
    align-items: center;
    gap: 8px;
  }
</style>
