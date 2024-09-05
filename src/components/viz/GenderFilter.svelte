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
      {gender.value}
    </div>
  {/each}
</div>

<style>
  .filter-content {
    display: flex;
    background-color: #373737;
    gap: 2px;
    padding: 2px;
    width: fit-content;
    margin-bottom: 8px;
  }

  .filter-content .gender-button {
    height: 50px;
    width: 70px;
    background-color: #555555;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
  }
  .filter-content .gender-button.selected {
    background-color: #313131;
    color: #ffb997;
  }
</style>
