<p>Filip</p>


<script>
    import { onMount } from 'svelte';
  
    let title = '';
    let movieInfo = null;
    let error = null;
  
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
              poster: data.poster,
              // Add more fields as needed
            };
            error = null;
          } else {
            movieInfo = null;
            error = `Error: ${data.Error}`;
          }
        })
        .catch(error => {
          movieInfo = null;
          error = `Error fetching data: ${error}`;
        });
    }
  
    onMount(() => {
      // Example usage
      getMovieInfo('Inception');
    });
  </script>
  
  <style>
    /* Add your styles here */
  </style>
  
  <main>
    <h1>Movie Search</h1>
  
    <input bind:value={title} placeholder="Enter movie title" />
  
    <button on:click={getMovieInfo}>Search</button>
  
    {#if movieInfo}
      <div>
        <h2>{movieInfo.title}</h2>
        <p>Year: {movieInfo.year}</p>
        <p>Genre: {movieInfo.genre}</p>
        <p>Runtime: {movieInfo.runtime}</p>
        <p>Poster: <img src="movieInfo.poster" alt=""> </p>
        <!-- Add more fields as needed -->
      </div>
    {:else if error}
      <p>{error}</p>
    {/if}
  </main>