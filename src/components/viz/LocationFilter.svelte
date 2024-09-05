<script>
  export let selectedLocation;
  let dropdownOpened = false;
  const locations = [
    "Bath",
    "Bournemouth",
    "Cambridge",
    "Chelmsford",
    "Colchester",
    "Ipswich",
    "Lincoln",
    "Milton Keynes",
    "Norwich",
    "Peterborough",
    "Romford",
    "Salisbury",
    "St Albans",
    "Stevenage",
  ];
</script>

<div class="location-container">
  {#if selectedLocation === null}
    <div
      class="location-button"
      role="button"
      tabindex="0"
      on:click={() => (dropdownOpened = !dropdownOpened)}
      on:keydown={() => (dropdownOpened = !dropdownOpened)}
    >
      <div>Select a location</div>
      <div>▽</div>
    </div>
  {:else}
    <div
      class="location-button"
      role="button"
      tabindex="0"
      on:click={() => (dropdownOpened = !dropdownOpened)}
      on:keydown={() => (dropdownOpened = !dropdownOpened)}
    >
      <div>
        {selectedLocation}
      </div>
      <div
        role="button"
        tabindex="0"
        on:click={() => {
          selectedLocation = null;
          dropdownOpened = false;
        }}
        on:keydown={() => {
          selectedLocation = null;
          dropdownOpened = false;
        }}
      >
        ✕
      </div>
    </div>
  {/if}

  {#if dropdownOpened}
    <div class="list">
      {#each locations as location}
        <div
          role="button"
          tabindex="0"
          on:click={() => {
            selectedLocation = location;
            dropdownOpened = false;
          }}
          on:keydown={() => {
            selectedLocation = location;
            dropdownOpened = false;
          }}
        >
          {location}
        </div>
      {/each}
    </div>{/if}
</div>

<style>
  .location-container {
    position: relative;
    background-color: grey;
    padding: 4px 8px;
    border-radius: 8px;
    width: 180px;
  }

  .location-container .location-button {
    display: flex;
    justify-content: space-between;
  }

  .location-container .list {
    position: absolute;
    left: 0;
    top: 38px;
    width: 100%;
    background-color: white;
    color: black;
  }

  .location-container .list div {
    padding: 2px 4px;
  }
</style>
