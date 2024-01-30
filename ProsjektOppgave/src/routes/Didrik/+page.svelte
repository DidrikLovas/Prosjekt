<script>
    const apiKey = '6dab94de';
    const baseUrl = 'http://www.omdbapi.com/';
    let img_url = ""
    function getMovieInfo(title) {
        const apiUrl = `${baseUrl}?apikey=${apiKey}&t=${encodeURIComponent(title)}`;

        fetch(apiUrl)
            .then(response => response.json())
            .then(data => {
                if (data.Response === 'True') {
                    console.log(`Title: ${data.Title}`);
                    console.log(`Year: ${data.Year}`);
                    console.log(`Genre: ${data.Genre}`);
                    console.log(`Director: ${data.Director}`);
                    console.log(`Handling: ${data.Plot}`);
                    img_url = data.Poster;
                } else {
                    console.error(`Error: ${data.Error}`);
                }
            })
            .catch(error => {
                console.error('Error fetching data:', error);
            });
    }

    // Example usage
    getMovieInfo('Matrix');
</script>
<img src="{img_url}" alt="Movie poster">