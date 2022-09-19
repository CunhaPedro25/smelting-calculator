<script>
  import furnaceLogo from "./assets/furnace.webp"
  import blastLogo from "./assets/blast.webp"
  import smokerLogo from "./assets/smoker.webp"
  import moment from "moment"

  let nStacks = 0
  let nItems = 0
  let nFurnaces = 1
  let selectedFurnace = 0

  function select(furnaceID) {
    selectedFurnace = furnaceID
  }

  let timeLeft = ""

  function calculateTime(_stacks, _items, _nFurnaces, _selectedFurnace) {
    let secondsPerItem = 10

    _items = _items + (_stacks * 64)

    let time = (secondsPerItem * _items) / _nFurnaces

    if(_selectedFurnace === 1){
      time = time / 2
    }

    timeLeft = moment.utc(time * 1000).format('HH:mm:ss')
  }
</script>

<main>
  <div class="flex w-screen h-screen justify-center items-center">
    <div>
      <div class="flex flex-row w-full justify-evenly">
        <button class:selected={selectedFurnace === 0}
                on:click={() => {select(0)}}>
          <img class="h-8" src={furnaceLogo} alt="Furnace">
        </button>
        <button class="flex flex-row gap-2"
                class:selected={selectedFurnace === 1}
                on:click={() => {select(1)}}>
          <img class="h-8" src={blastLogo} alt="Blast Furnace">
          <img class="h-8" src={smokerLogo} alt="Smoker">
        </button>
      </div>
      <div>
        <label for="stacks">Furnaces</label>
        <input type="number" id="furnaces" bind:value={nFurnaces} min="1">
      </div>
      <div>
        <label for="stacks">Stacks</label>
        <input type="number" id="stacks" bind:value={nStacks} min="0">
      </div>
      <div>
        <label for="items">Items</label>
        <input type="number" id="items" bind:value={nItems} min="0">
      </div>
      <div>
        <button on:click={() => {calculateTime(nStacks,nItems,nFurnaces,selectedFurnace)}}>
          Calculate
        </button>
      </div>
      {#if timeLeft}
        <p>{timeLeft}</p>
      {/if}
    </div>
  </div>
</main>
