<!-- App.svelte -->
<script>
    import { onMount } from 'svelte';
  
    let title = '';
    let movieInfo = null;
    let error = null;
    let buttonClicked = false
  
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
              type: data.Type,
              plot: data.Plot,
              resp: data.response
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
    main {
      display: flex;
      flex-direction: column;
      align-items: center;
      margin: 20px;
    }
  
    h1 {
      text-align: center;
      color: #333;
    }
  
    input {
      padding: 10px;
      margin: 10px 0;
      font-size: 16px;
    }
  
    button {
      padding: 10px;
      background-color: #007bff;
      color: #fff;
      font-size: 16px;
      cursor: pointer;
      border: none;
    }
  
    button:hover {
      background-color: #0056b3;
    }
  
    div {
      margin-top: 20px;
      text-align: center;
    }
  
    h2 {
      color: #333;
    }
  
    p {
      margin: 5px 0;
      color: #555;
    }
  
    img {
      max-width: 100%;
      height: auto;
      margin-top: 10px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    }
  
    /* Add more styles as needed */
  </style>
  
  <main>
    <h1>Movie/Series Search</h1>
  
    <input bind:value={title} placeholder="Enter title" />
  
    <button on:click={getMovieInfo} on:click={buttonClicked = true}>Search</button>
  
    {#if movieInfo}
      <div>
        <h2>{movieInfo.title}</h2>
        <p>Year: {movieInfo.year}</p>
        <p>Type: {movieInfo.type}</p>
        <p>Genre: {movieInfo.genre}</p>
        <p>Plot: {movieInfo.plot}</p>
        <p>Runtime: {movieInfo.runtime}</p>
        <img src={movieInfo.poster} alt="Filmplakat">
      </div>
      {:else if buttonClicked && error}
      <p>{error}</p>
    {/if}
  </main>
  