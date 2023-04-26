<script>

  import Character from "./lib/Character.svelte";

  let characters = [];
  let page = 1;

  async function loadCharaacter() {
    const response = await fetch(
      "https://rickandmortyapi.com/api/character?page=" + page
    );
    const data = await response.json();
    characters = data.results;
  }
  loadCharaacter();

  function nextPage() {
    page++;
    loadCharaacter()
  }

  function previousPage() {
    page--;
    loadCharaacter()
  }
</script>

<h1 class="title">Rick And Morty Svelte</h1>

<div class="container">

  <div class="btns">
    <button on:click={previousPage} disabled={page === 1}>Previous</button>
    <button on:click={nextPage}>next</button>
  </div>

  <div class="grid">
    {#each characters as character}
      <Character character={character}/>
    {/each}
  </div>
</div>
