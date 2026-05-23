<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Ultimate Movie Explorer</title>

  <!-- Bootstrap -->
  <link
    rel="stylesheet"
    href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css"
  >

  <!-- Google Font -->
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">

  <style>

    *{
      margin:0;
      padding:0;
      box-sizing:border-box;
      font-family:'Poppins',sans-serif;
    }

    body{
      background:#0f172a;
      color:white;
      overflow-x:hidden;
    }

    /* Navbar */

    .navbar{
      background:#111827;
      padding:15px 30px;
    }

    .navbar-brand{
      color:#facc15 !important;
      font-size:30px;
      font-weight:700;
    }

    .search-box{
      width:300px;
      border-radius:30px;
      border:none;
      padding:10px 20px;
      outline:none;
    }

    /* Hero Section */

    .hero{
      text-align:center;
      padding:60px 20px;
      background:linear-gradient(to right,#111827,#1e293b);
    }

    .hero h1{
      font-size:4rem;
      color:#facc15;
      font-weight:700;
    }

    .hero p{
      color:#cbd5e1;
      margin-top:15px;
      font-size:1.2rem;
    }

    .hero button{
      margin-top:20px;
      background:#facc15;
      border:none;
      padding:12px 30px;
      border-radius:30px;
      font-weight:600;
      transition:0.3s;
    }

    .hero button:hover{
      transform:scale(1.05);
      background:#eab308;
    }

    /* Movie Cards */

    .movie-card{
      background:#1e293b;
      border:none;
      border-radius:20px;
      overflow:hidden;
      transition:0.4s;
      box-shadow:0 10px 20px rgba(0,0,0,0.4);
    }

    .movie-card:hover{
      transform:translateY(-10px);
    }

    .movie-card img{
      width:100%;
      height:450px;
      object-fit:cover;
    }

    .card-body{
      padding:20px;
    }

    .movie-title{
      color:#facc15;
      font-size:24px;
      font-weight:700;
    }

    .rating{
      color:#38bdf8;
      font-weight:600;
      margin-bottom:10px;
    }

    .genre{
      display:inline-block;
      background:#334155;
      padding:5px 12px;
      border-radius:20px;
      font-size:12px;
      margin-bottom:12px;
    }

    .description{
      color:#cbd5e1;
      font-size:14px;
      min-height:70px;
    }

    .btn-watch{
      background:#22c55e;
      color:white;
      border:none;
      padding:10px 18px;
      border-radius:10px;
      margin-right:10px;
      font-weight:600;
    }

    .btn-watch:hover{
      background:#16a34a;
    }

    .btn-delete{
      background:#ef4444;
      color:white;
      border:none;
      padding:10px 18px;
      border-radius:10px;
      font-weight:600;
    }

    .btn-delete:hover{
      background:#dc2626;
    }

    footer{
      margin-top:50px;
      text-align:center;
      padding:30px;
      color:#94a3b8;
      background:#111827;
    }

  </style>
</head>

<body>

  <!-- Navbar -->

  <nav class="navbar navbar-expand-lg">
    <a class="navbar-brand" href="#">🎬 MovieVerse</a>

    <input
      type="text"
      id="searchInput"
      class="search-box ml-auto"
      placeholder="Search movie..."
      onkeyup="searchMovies()"
    >
  </nav>

  <!-- Hero -->

  <section class="hero">

    <h1>Unlimited Movies</h1>

    <p>
      Explore trending Hollywood movies with beautiful UI ✨
    </p>

    <button onclick="refreshMovies()">
      🔄 Refresh Movies
    </button>

  </section>

  <!-- Movies -->

  <div class="container mt-5">

    <div class="row" id="movieContainer"></div>

  </div>

  <!-- Footer -->

  <footer>
    Created with HTML • CSS • Bootstrap • JavaScript 🚀
  </footer>

  <script>

    const movies = [

      {
        title:"Inception",
        rating:"⭐ 8.8",
        genre:"Sci-Fi",
        image:"https://image.tmdb.org/t/p/w500/9gk7adHYeDvHkCSEqAvQNLV5Uge.jpg",
        description:"A skilled thief enters dreams to steal secrets."
      },

      {
        title:"Interstellar",
        rating:"⭐ 8.7",
        genre:"Adventure",
        image:"https://image.tmdb.org/t/p/w500/gEU2QniE6E77NI6lCU6MxlNBvIx.jpg",
        description:"Explorers travel through a wormhole in space."
      },

      {
        title:"The Dark Knight",
        rating:"⭐ 9.0",
        genre:"Action",
        image:"https://image.tmdb.org/t/p/w500/qJ2tW6WMUDux911r6m7haRef0WH.jpg",
        description:"Batman battles the Joker in Gotham City."
      },

      {
        title:"Avengers Endgame",
        rating:"⭐ 8.4",
        genre:"Marvel",
        image:"https://image.tmdb.org/t/p/w500/or06FN3Dka5tukK1e9sl16pB3iy.jpg",
        description:"The Avengers assemble to defeat Thanos."
      },

      {
        title:"Spider-Man No Way Home",
        rating:"⭐ 8.3",
        genre:"Superhero",
        image:"https://image.tmdb.org/t/p/w500/1g0dhYtq4irTY1GPXvft6k4YLjm.jpg",
        description:"Spider-Man faces villains from multiple universes."
      },

      {
        title:"Joker",
        rating:"⭐ 8.5",
        genre:"Thriller",
        image:"https://image.tmdb.org/t/p/w500/udDclJoHjfjb8Ekgsd4FDteOkCU.jpg",
        description:"A failed comedian slowly turns into Joker."
      },

      {
        title:"Titanic",
        rating:"⭐ 7.9",
        genre:"Romance",
        image:"https://image.tmdb.org/t/p/w500/9xjZS2rlVxm8SFx8kPC3aIGCOYQ.jpg",
        description:"A romantic story aboard the Titanic ship."
      },

      {
        title:"John Wick",
        rating:"⭐ 7.4",
        genre:"Action",
        image:"https://image.tmdb.org/t/p/w500/fZPSd91yGE9fCcCe6OoQr6E3Bev.jpg",
        description:"An ex-hitman seeks revenge against gangsters."
      },

      {
        title:"Doctor Strange",
        rating:"⭐ 7.5",
        genre:"Fantasy",
        image:"https://image.tmdb.org/t/p/w500/uGBVj3bEbCoZbDjjl9wTxcygko1.jpg",
        description:"A surgeon learns mystical arts to save reality."
      }

    ];

    const container = document.getElementById("movieContainer");

    function displayMovies(movieArray){

      container.innerHTML = "";

      movieArray.forEach((movie,index)=>{

        container.innerHTML += `

          <div class="col-lg-4 col-md-6 mb-4">

            <div class="card movie-card h-100">

              <img src="${movie.image}" alt="${movie.title}">

              <div class="card-body">

                <h3 class="movie-title">${movie.title}</h3>

                <p class="rating">${movie.rating}</p>

                <span class="genre">${movie.genre}</span>

                <p class="description">
                  ${movie.description}
                </p>

                <button
                  class="btn-watch"
                  onclick="watchMovie('${movie.title}')"
                >
                  ▶ Watch
                </button>

                <button
                  class="btn-delete"
                  onclick="deleteMovie(${index})"
                >
                  🗑 Delete
                </button>

              </div>

            </div>

          </div>

        `;
      });

    }

    displayMovies(movies);

    function watchMovie(title){
      alert("Now Playing: " + title + " 🎥");
    }

    function deleteMovie(index){
      movies.splice(index,1);
      displayMovies(movies);
    }

    function refreshMovies(){
      alert("Movies refreshed successfully 🚀");
      displayMovies(movies);
    }

    function searchMovies(){

      const searchValue =
        document.getElementById("searchInput")
        .value
        .toLowerCase();

      const filteredMovies = movies.filter(movie =>
        movie.title.toLowerCase().includes(searchValue)
      );

      displayMovies(filteredMovies);

    }

  </script>

</body>
</html>
