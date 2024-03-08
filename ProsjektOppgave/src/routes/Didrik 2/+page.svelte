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
  </script>

  