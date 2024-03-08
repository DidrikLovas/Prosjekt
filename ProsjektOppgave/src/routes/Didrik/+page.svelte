<!-- App.svelte -->
<script>
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
    function handleRating(stars) {
    rating = stars;
  }

  const alternativer = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10].reverse();
    
    let midlertidigVurdering = 5;
    //Math.round(gjennomsnitt)

  </script>
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
  <!-- App.svelte -->
<style>
    nav {
    background-color: #333;
    padding: 10px 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }

  .logo {
    color: #fff;
    font-size: 24px;
    font-weight: bold;
    text-decoration: none;
  }

  .nav-links {
    display: flex;
    list-style-type: none;
    margin: 0;
    padding: 0;
  }

  .nav-links li {
    margin-right: 20px;
  }

  .nav-links a {
    color: #fff;
    text-decoration: none;
    font-size: 16px;
    transition: color 0.3s ease;
  }

  .nav-links a:hover {
    color: #007bff;
  }


.dropdown {
  position: relative;
  display: inline-block;
  cursor: pointer;
}

.dropdown-content {
  display: none;
  position: absolute;
  left: -2vw;
  background-color: #f1f1f1;
  width:100px;
  box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
  z-index: 1;
  margin: 0px;
}

.dropdown-content a {
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
}

.dropdown-content a:hover {background-color: #ddd;}

.dropdown:hover .dropdown-content {display: flex;
  flex-direction: column;
}
.stjerneVurderingContainer {
        display: flex;
        position: relative;
        flex-direction: row-reverse; /* Change from 'row' to 'row-reverse' */
        justify-content: center;
        width: 60%;
        top: -3%;
        margin-left: 40px;
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
    main {
      display: flex;
      flex-direction: column;
      align-items: center;
      margin: 20px;
    }
  
    h1 {
      font-size: 24px;
      color: #333;
      margin-bottom: 20px;
    }
  
    input {
      padding: 10px;
      margin: 10px 0;
      font-size: 16px;
      border: 1px solid #ddd;
      border-radius: 4px;
      width: 300px;
      box-sizing: border-box;
    }
  
    button {
      padding: 10px 20px;
      background-color: #007bff;
      color: #fff;
      font-size: 16px;
      cursor: pointer;
      border: none;
      border-radius: 4px;
    }
  
    button:hover {
      background-color: #0056b3;

    }
  
    div {
      margin-top: 20px;
      text-align: center;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
      padding: 20px;
      border-radius: 4px;
      background-color: #fff;
      width: 300px;
      box-sizing: border-box;
    }
  
    h2 {
      color: #333;
      font-size: 20px;
      margin-bottom: 10px;
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
      border-radius: 4px;
    }
  
    p.error {
      color: #ff4d4f;
      margin-top: 10px;
    }
  </style>
  
  <nav>
    <a class="logo" href="#">Your Logo</a>
    <ul class="nav-links">
      <li><a href="#">Home</a></li>
      <li><a href="#">About</a></li>
      <li class="dropdown">
          <a>More</a>
          <div class="dropdown-content">
            <a href="#">Link 1</a>
            <a href="#">Link 2</a>
            <a href="#">Link 3</a>
          </div>
    </ul>
  </nav>
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
        {#if !(movieInfo.plot == "N/A")}
        <p>Plot: {movieInfo.plot}</p>
        {/if}
        {#if !(movieInfo.runtime == "N/A")}
        <p>Runtime: {movieInfo.runtime}</p>
        {/if}
        {#if !(movieInfo.poster == "N/A")}
        <img src={movieInfo.poster} alt="Movie poster">
        {/if}

      <span class="stjerneVurderingContainer">
        {#each alternativer as alternativ}
         <input
            value={alternativ}
            bind:group={midlertidigVurdering}
            type="radio"
            name="star"
            id={alternativ.toString()}
          /><label for={alternativ.toString()} />
        {/each}
      </span>
    </div>
    {:else if buttonClicked && error}
        <p class="error">{error}</p>
      {/if}
  </main>
