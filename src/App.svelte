<script>

  import Character from './lib/Character.svelte'

  let characters = [];
  let page = 1; // Contador de pagina.
  
  async function loadCharacters() { 
    const response = await fetch('https://rickandmortyapi.com/api/character?page=' + page)
    const data = await response.json()
    console.log(data)
    characters = data.results;
  }
  loadCharacters();

  function nextPage() { // próximo
    page++;
    loadCharacters();
  }

  function previousPage() { // anterior
    page--;
    loadCharacters();
  }

</script>

<h1 class="title">Rick y Morty Svelte</h1>

<div class="container">

  <div class="btns">
    <button class="btn" on:click={previousPage} disabled={page === 1} >Anterior</button>
    <button class="btn" on:click={nextPage}>Próximo</button>
  </div>

  <div class="grid">
    {#each characters as character}
      <Character character={character}/>
    {/each}
  </div>

</div>