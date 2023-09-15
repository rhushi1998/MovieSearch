# MovieSearch

This is a simple movie search web that allows users to search for movies by name. The app is built using HTML, CSS, and JavaScript

# Hostted Link :-

## Html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Movie Search</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <div id="container">
      <input
        type="text"
        id="movieSearch"
        placeholder="Enter Movie Name here..."
      />
      <button id="search">Search</button>
    </div>
    <div id="root"></div>
    <script src="index.js"></script>
  </body>
</html>

## css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  #container {
    margin-top: 40px;
    text-align: center;
  }
  #movieSearch {
    padding: 15px 100px;
    border-radius: 10px;
    border: 1px solid black;
    font-size: 20px;
    font-weight: 900;
  }
  #search {
    padding: 15px 20px;
    border-radius: 10px;
    border: 1px solid antiquewhite;
    font-weight: 900;
    font-size: 20px;
  }
  #root {
    margin-top: 30px;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 15px;
    align-items: center;
    justify-content: center;
  }
  #rootDiv {
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
  }
  
  img {
    border-radius: 10px;
  }
  h3 {
    text-transform: uppercase;
    font-weight: 900;
    font-size: 20px;
  }
  #YearDiv {
    font-size: 30px;
    font-weight: 900;
  }

  ## Js

  const movie = document.getElementById("movieSearch");
const btn = document.getElementById("search");
const root = document.getElementById("root");
async function getMovie() {
  root.innerText = "";
  let movieName = movie.value;
  try {
    let response = await fetch(
      `https://www.omdbapi.com/?&apikey=f8ec2e0&s=${movieName}`
    );
    let data = await response.json();
    console.log(data);
    const movieList = data.Search;
    console.log(movieList);

    movieList.forEach((movie) => {
      console.log(movie);
      getMovies(movie);
    });

    function getMovies(movie) {
      const newDiv = document.createElement("div");
      newDiv.id = "rootDiv";
      newDiv.innerHTML = `
      <div id ="imgDiv"><img src = ${movie.Poster}</div>
      <h3 id ="titleDiv">${movie.Title} </h3></br>
      <p id ="YearDiv">${movie.Year}</p>
      `;
      root.appendChild(newDiv);
    }
    movie.value = "";
  } catch (error) {
    console.log(error, "error");
  }
}

btn.addEventListener("click", getMovie);
