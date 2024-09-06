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

<!-- Button with two use cases -->
<div
  class="location-container"
  style={selectedLocation
    ? "background-color: #313131;"
    : "background-color: #666"}
>
  {#if selectedLocation === null}
    <div
      class="location-button"
      role="button"
      tabindex="0"
      on:click={() => (dropdownOpened = !dropdownOpened)}
      on:keydown={() => (dropdownOpened = !dropdownOpened)}
    >
      <div>Select a loc.</div>
      <div style="font-size:12px;">▽</div>
    </div>
  {:else}
    <div
      class="location-button"
      role="button"
      tabindex="0"
      on:click={() => (dropdownOpened = !dropdownOpened)}
      on:keydown={() => (dropdownOpened = !dropdownOpened)}
    >
      <div
        style="color: #ffb997; font-weight:700;     text-shadow: 0px 0px 4px #ffba977d;
"
      >
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

  <!-- Dropdown list -->
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

    padding: 4px 8px;
    border-radius: 8px;
    width: 160px;
    cursor: pointer;
  }

  .location-container .location-button {
    display: flex;
    justify-content: space-between;
    align-items: center;
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
  .location-container .list > div:hover {
    font-weight: 700;
  }
</style>
