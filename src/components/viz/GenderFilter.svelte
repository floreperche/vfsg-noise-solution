<script>
  export let genderValues;
</script>

<div class="filter-content">
  {#each genderValues as gender}
    <div
      class={gender.selected ? "gender-button selected" : "gender-button"}
      role="button"
      tabindex="0"
      on:click={() => (gender.selected = !gender.selected)}
      on:keydown={() => (gender.selected = !gender.selected)}
    >
      <p>{gender.value}</p>
    </div>
  {/each}
</div>

<style>
  .filter-content {
    display: flex;
    background-color: #373737;
    gap: 4px;
    padding: 4px;
    width: fit-content;
    margin-bottom: 8px;
    border-radius: 4px;
    box-shadow: inset 2px 2px 20px rgba(0, 0, 0, 0.458);
  }

  .filter-content .gender-button {
    height: 50px;
    width: 70px;
    background-color: #555555;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    box-shadow: inset 4px 6px 10px 0 rgba(255, 255, 255, 0.2);
    border-radius: 3px;
    cursor: pointer;
  }
  .filter-content .gender-button.selected {
    background-color: #313131;
    color: #ffb997;
    box-shadow: inset 4px 6px 15px 0 rgba(0, 0, 0, 0.439);
  }

  .filter-content .gender-button.selected p {
    font-weight: 700;
    text-shadow: 0px 0px 4px #ffba977d;
  }
</style>
