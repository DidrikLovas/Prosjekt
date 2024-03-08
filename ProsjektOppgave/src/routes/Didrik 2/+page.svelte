<script>
    import { onMount } from 'svelte';
  
    let api_key = '6dab94de';
    let search_query = '';
    let movies = [];
  
    const searchMovies = async () => {
      const url = `http://www.omdbapi.com/?apikey=${api_key}&s=${search_query}`;
      try {
        const response = await fetch(url);
        if (response.ok) {
          const data = await response.json();
          movies = data.Search || [];
        } else {
          console.error(`Feil ved henting av data. Statuskode: ${response.status}`);
        }
      } catch (error) {
        console.error('Noe gikk galt under forespørselen:', error);
      }
    };
  
    onMount(() => {
      // Initier søk når komponenten blir montert for første gang
      searchMovies();
    });
  </script>
  
  <main>
    <h1>Søk etter filmer</h1>
  
    <input bind:value={search_query} placeholder="Skriv inn søkeord" />
  
    <button on:click={searchMovies}>Søk</button>
  
    {#if movies.length > 0}
      <ul>
        {#each movies as movie}
          <li>
            <p>Tittel: {movie.Title}, År: {movie.Year}, IMDb-ID: {movie.imdbID}</p>
          </li>
        {/each}
      </ul>
    {:else}
      <p>Ingen resultater funnet.</p>
    {/if}
  </main>
  
  <style>
    main {
      text-align: center;
      margin: 2rem;
    }
  
    input, button {
      margin-bottom: 1rem;
    }
  </style>
  