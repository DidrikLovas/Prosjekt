<script>
  import { onMount } from 'svelte';

  let title = '';
  let movieInfo = null;
  let error = null;
  let rating = 0; // Initial rating

  const apiKey = '6dab94de'; // Replace with your actual OMDb API key
  const baseUrl = 'http://www.omdbapi.com/';

  function getMovieInfo() {
    const apiUrl = `${baseUrl}?apikey=${apiKey}&t=${encodeURIComponent(title)}`;

    fetch(apiUrl)
      .then(response => response.json())
      .then(data => {
        if (data.Response === 'True') {
          movieInfo = {
            title: data.Title,
            year: data.Year,
            genre: data.Genre,
            runtime: data.Runtime,
            poster: data.Poster,
            // Add more fields as needed
          };
          error = null;
        } else {
          movieInfo = null;
          error = `Filmen finnes ikke`;
        }
      })
      .catch(error => {
        movieInfo = null;
        error = `Error fetching data: ${error}`;
      });
  }

  function handleRating(stars) {
    rating = stars;
  }

  onMount(() => {
    // Example usage
    getMovieInfo('Inception');
  });

  const alternativer = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10].reverse();
    
    let midlertidigVurdering = 5;
    //Math.round(gjennomsnitt)
  
</script>

<div class="stjerneVurderingContainer">
  {#each alternativer as alternativ}
    <input
      value={alternativ}
      bind:group={midlertidigVurdering}
      type="radio"
      name="star"
      id={alternativ.toString()}
    /><label for={alternativ.toString()} />
  {/each}
</div>

<head>
  <link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css"
/>
<link
  href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.missing_component.css"
  rel="stylesheet"
/>
</head>


<style>
  main {
    display: grid;
    grid-template-rows: auto 1fr auto;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
    padding: 20px;
  }

  .stjerneVurderingContainer {
    display: flex;
    position: relative;
    flex-direction: row-reverse;
    align-items: center;
    width: 100%; /* Adjust as needed */
    margin: 0;
    padding: 0;
  }

  .stjerneVurderingContainer input {
    display: none;
  }

  .stjerneVurderingContainer label {
    display: block;
    cursor: pointer;
    width: 2vh;
  }

  .stjerneVurderingContainer label:before {
    content: "\f005";
    font-family: fontAwesome;
    position: relative;
    display: block;
    font-size: 2vh;
  }

  .stjerneVurderingContainer label:after {
    content: "\f005";
    font-family: fontAwesome;
    position: absolute;
    display: block;
    font-size: 2vh;
    color: orange;
    top: 0;
    opacity: 0;
    transition: 0.5s;
    text-shadow: 0 2px 5px rgba(0, 0, 0, 0.5);
  }

  .stjerneVurderingContainer label:hover:after,
  .stjerneVurderingContainer input:hover ~ label:after,
  .stjerneVurderingContainer input:checked ~ label:after {
    opacity: 1;
  }

  /* Add more styling as needed */

  main img {
    grid-row: 1 / span 3;
    grid-column: 2;
    max-width: 100%;
    height: auto;
  }

  main h1,
  main input,
  main button {
    grid-column: span 2;
  }


  

  .error-message {
    grid-column: span 2;
    color: red;
  }

</style>

<main>
  <h1>Movie Search</h1>

  <input bind:value={title} placeholder="Søk på en film" />

  <button on:click={getMovieInfo}>Search</button>

  {#if title === '' && !movieInfo && !error}
    <p>Søk på en film</p>
  {:else if error}
    <p class="error-message">{error}</p>
  {:else if movieInfo}
    <div>
      <h2>{movieInfo.title}</h2>
      <p>Year: {movieInfo.year}</p>
      <p>Genre: {movieInfo.genre}</p>
      <p>Runtime: {movieInfo.runtime}</p>
      <p>Poster: <img src={movieInfo.poster} alt="" /> </p>
      
      <div class="stjerneVurderingContainer">
        {#each alternativer as alternativ}
          <input
            value={alternativ}
            bind:group={midlertidigVurdering}
            type="radio"
            name="star"
            id={alternativ.toString()}
          /><label for={alternativ.toString()} />
        {/each}
      </div>

      <!-- Add more fields as needed -->
    </div>
  {/if}

  
  <img src="src/routes/Filip/logo1.png" alt="">
</main>


