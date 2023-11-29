
# ✨ Movies Api 






```c#


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
    <title>Styled Cards with Bootstrap</title>
</head>
<body>
    <nav class="navbar navbar-dark">
        <div class="container">
            <span class="navbar-brand" style="color:red ; font-weight:700 ; font-size :32px">Netflix</span>
        </div>
    </nav>

    <div class="container mt-5">
        <div class="row">
            <div class="col-md-6 offset-md-3">
                <div class="input-group mb-3">
                    <input type="text" class="form-control" placeholder="Search..." aria-label="Search" aria-describedby="search-button" id="moveName">
                    <div class="input-group-append">
                        <button class="btn btn-outline-secondary" type="button" id="btn" onclick="getMovies()">Search</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div class=" mt-8" id="movieContainer">
        <div class="row" id="movieRow">
            <!-- Movie cards will be added dynamically here -->
        </div>
    </div>

    <div class="modal fade" id="movieModal" tabindex="-1" role="dialog" aria-labelledby="movieModalLabel" aria-hidden="true">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="movieModalLabel">Movie Details</h5>
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                        <span aria-hidden="true">&times;</span>
                    </button>
                </div>
                <div class="modal-body" id="modalBody">
                    <!-- Movie details will be added dynamically here -->
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
                </div>
            </div>
        </div>
    </div>

    <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js"></script>

</body>
</html>


```
```js
    <script>
        let key = "7cc4a6dd";

        let getMovies = () => {
            let movieName = document.getElementById("moveName").value;
            let url = `https://www.omdbapi.com/?s=${movieName}&apiKey=${key}`;

            fetch(url)
                .then((res) => res.json())
                .then((data) => {
                    if (data.Response === "True") {
                        displayMovies(data.Search);
                    } else {
                        alert("No movies found!");
                    }
                })
                .catch((error) => {
                    console.error("Error fetching movies:", error);
                });
        };

        let displayMovies = (movies) => {
            let movieContainer = document.getElementById("movieContainer");
            let movieRow = document.getElementById("movieRow");

            // Clear previous search results
            movieRow.innerHTML = "";

            // Create cards for each movie
            movies.forEach((movie) => {
                let card = document.createElement("div");
                card.classList.add("col-md-3");
                card.innerHTML = `
                            <div class="card">
                                <img src="${movie.Poster}" class="card-img-top" alt="Movie Poster">
                                <div class="card-body">
                                    <h5 class="card-title">${movie.Title}</h5>
                                    <p class="card-text">${movie.Year}</p>
                                    <button class="btn btn-primary" data-toggle="modal" data-target="#movieModal" onclick="getMovieDetails('${movie.imdbID}')">See Details</button>
                                </div>
                            </div>
                        `;

                // Append the card to the movieRow
                movieRow.appendChild(card);
            });
        };

        let getMovieDetails = (imdbID) => {
            let url = `https://www.omdbapi.com/?i=${imdbID}&apiKey=${key}`;

            fetch(url)
                .then((res) => res.json())
                .then((data) => {
                    displayMovieDetails(data);
                })
                .catch((error) => {
                    console.error("Error fetching movie details:", error);
                });
        };

        let displayMovieDetails = (movie) => {
            let modalBody = document.getElementById("modalBody");
            modalBody.innerHTML = `
                        <img src="${movie.Poster}" class="img-fluid mb-3" alt="Movie Poster">
                        <p><strong>Title:</strong> ${movie.Title}</p>
                        <p><strong>Year:</strong> ${movie.Year}</p>
                        <p><strong>Genre:</strong> ${movie.Genre}</p>
                        <p><strong>Plot:</strong> ${movie.Plot}</p>
                        <p><strong>Director:</strong> ${movie.Director}</p>
                        <!-- Add more details as needed -->
                    `;
        };
    </script>
```
