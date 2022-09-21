<script>
  import background from "./assets/background.png"

  import coal from "./assets/coal.png"
  import ironIngot from "./assets/iron_ingot.png"
  import stack from "./assets/stack.png"

  import furnaceLogo from "./assets/furnace.webp"
  import blastLogo from "./assets/blast.webp"
  import smokerLogo from "./assets/smoker.webp"
  import fire from "./assets/fire.png"
  import arrow from "./assets/arrow.png"

  import moment from "moment"

  let nStacks = 0
  let nItems = 0
  let nFurnaces = 1
  let selectedFurnace = 0

  let timeLeft = "00:00:00"

  function calculateTime() {
    let secondsPerItem = 10
    let _nItems

    _nItems = nItems + (nStacks * 64)

    if(nFurnaces === 0) nFurnaces = 1

    

    let time = nFurnaces === null ? 0 : (secondsPerItem * _nItems) / nFurnaces

    if(selectedFurnace === 1){
      time = time / 2
    }

    timeLeft = moment.utc(time * 1000).format('HH:mm:ss')
  }
</script>

<main>
  <div class="absolute h-screen w-screen pixelated" style="background-image: url({background}); background-size: 5%;"></div>

  <div class="relative flex w-screen h-screen justify-center items-center p-2 bg-black/30">
    <div class="p-[.1rem] bg-black pixel-corners">
      <div class="flex flex-col pixel-corners p-4 gap-4 bg-[#c6c6c6] border-[.2rem] border-l-white border-t-white border-r-[#555555] border-b-[#555555]">
        <div class="flex justify-center items-center gap-1">
          <div class="flex gap-3 pr-2">
            <input class="bg-white relative w-8 bottom-auto right-auto" type="number" id="furnaces" bind:value={nFurnaces} on:input={calculateTime} min="1">
            <p>X</p>
          </div>
          
          <div class="button" class:selected={selectedFurnace === 0} on:click={()=>{selectedFurnace = 0; calculateTime()}}>
            <div class="background">
              <img class="h-12" src={furnaceLogo} alt="Furnace">
            </div>
          </div>
          <div class="button" class:selected={selectedFurnace === 1} on:click={()=>{selectedFurnace = 1; calculateTime()}}>
            <div class="background">
              <img class="h-12" src={blastLogo} alt="Blast Furnace">
              <img class="h-12" src={smokerLogo} alt="Smoker">
            </div>
          </div>
        </div>
      
        <div class="flex gap-2 justify-center items-center">
          <div class="flex flex-col gap-1 items-end">
            <div class="flex justify-center items-center gap-2">
              <div class="item-slot">
                <img class="h-12" src={stack} alt="stack">
                <label for="stacks" class="absolute h-full w-full z-10"></label>
                <input type="number" id="stacks" bind:value={nStacks} on:input={calculateTime} min="0">
              </div>
              <p class="text-3xl">+</p>
              <div class="item-slot">
                <img class="h-12" src={ironIngot} alt="ingot">
                <label for="items" class="absolute h-full w-full z-10"></label>
                <input type="number" id="items" bind:value={nItems} on:input={calculateTime} min="0">
              </div>
            </div>
            <div class="flex justify-center items-center pixelated h-12 w-12 p-0.5 mr-1">
              <img class="h-8" src={fire} alt="fire">
            </div>
            <div class="item-slot">
              <img class="h-12" src={coal} alt="coal">
            </div>
          </div>
          <div class="flex justify-center items-center h-12 p-1 pixelated">
            <img class="h-full" src={arrow} alt="arrow">
          </div>
          <p>{timeLeft}</p>
        </div>
      </div>
    </div>
  </div>
</main>