<script>
  let clicks = 100;
  let multiplier = 1;
  let workers = [];
  let worker_multiplier = 1;

  let upgrades = [
    { cost: 15, name: "Doubler", multiplier: 2, worker: 0 },
    { cost: 5, name: "Worker", multiplier: 0, worker: 1 },
  ];

  function increment() {
    clicks = clicks + multiplier;
    console.log("click" + clicks);
  }
</script>

<article>
  <header>
    <div class="grid">
      {#each upgrades as upgrade}
        <button
          class="upgrade"
          on:click={() => {
            if (clicks >= upgrade.cost) {
              if (upgrade.multiplier) {
                multiplier = multiplier * upgrade.multiplier;
                clicks -= upgrade.cost;
              }
              if (upgrade.worker && clicks) {
                worker_multiplier = worker_multiplier * 2;
                workers = [upgrade.name, ...workers];
                /* start "clicking" every 1000 ms */
                setInterval(increment, 1000);
                clicks -= upgrade.cost;
              }
            } else {
              alert("Click some more first!");
            }
          }}
        >
          <span>{upgrade.name}</span>
          <span>{upgrade.cost * worker_multiplier}</span>
        </button>
      {/each}
    </div>
  </header>
  <div class="game">
    <button on:click={increment} class="clicker">
      <span class="clicks">{clicks}</span>
      <span class="pointtext">PPC: {multiplier}</span>
    </button>
  </div>
  <footer>
    <div class="panelright">
      <div>
        <span>Workers</span>
        <hr />
        <div class="shop">
          {#each workers as worker}
            <div class="worker">{worker}</div>
          {/each}
        </div>
      </div>
      <hr />
    </div>
  </footer>
</article>

<style>
  .shop {
    display: grid;
    grid-auto-flow: row; /* default */
    gap: 8px;
    grid-template-rows: repeat(3, 1fr);
    grid-template-columns: repeat(3, 1fr);
  }

  .upgrade {
    width: 100%;
    height: 100%;
    border: 4px solid rgb(219, 16, 16);
    background-color: rgb(59, 183, 28);
    background-size: cover;
    background-image: url("data:image/jpeg;base64,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");
    place-items: center;
    place-content: center;
    display: flex;
    flex-direction: column;
  }

  .worker {
    width: 100%;
    height: 100%;
    border: 1px solid black;
    background-color: rgb(128, 141, 27);
    place-items: center;
    place-content: center;
    display: flex;
  }

  .game {
    height: 50vh;
    display: flex;
    flex-direction: column;
    place-items: center;
    place-content: center;
  }
  .clicker {
    clip-path: circle();
    display: flex;
    height: 100%;
    width: 100%;
    flex-direction: column;
    place-items: center;
    place-content: center;
    background-image: url("https://assets.bonappetit.com/photos/5ca534485e96521ff23b382b/4:3/w_3600,h_2700,c_limit/chocolate-chip-cookie.jpg");
    background-size: cover;
    background-position: 0px -100px;
  }

  .panelright {
    height: 100%;
    display: flex;
    flex-direction: column;
    gap: 16px;
  }

  .clicks {
    font-size: 100px;
  }

  .pointtext {
    color: brown;
    font-size: 25px;
    font-weight: bold;
  }
</style>
