<script>
    // Replace 'YOUR_API_KEY' with your actual OMDb API key
    const apiKey = '6dab94de';
    const baseUrl = 'http://www.omdbapi.com/';

    function getMovieInfo(title) {
        const apiUrl = `${baseUrl}?apikey=${apiKey}&t=${encodeURIComponent(title)}`;

        // Make a GET request to the OMDb API
        fetch(apiUrl)
            .then(response => response.json())
            .then(data => {
                if (data.Response === 'True') {
                    console.log(`Title: ${data.Title}`);
                    console.log(`Year: ${data.Year}`);
                    console.log(`Genre: ${data.Genre}`);
                    console.log(`Director: ${data.Director}`);
                    // Add more fields as needed
                } else {
                    console.error(`Error: ${data.Error}`);
                }
            })
            .catch(error => {
                console.error('Error fetching data:', error);
            });
    }

    // Example usage
    getMovieInfo('Inception');
</script>