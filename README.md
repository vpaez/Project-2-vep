# React Hackathon

![Homepage](/readme-images/homepage.png)


Web application powered by Deezer, a music streaming API. It allows users to search for artists and provides results sorted by albums, with album covers, tracklisting and samples.

### Timeframe
1.5 day



## Technologies used

* React
* Axios
* Javascript
* SCSS
* Bulma
* HTML
* Git
* Webpack
* Ajax
* Deployment via heroku
* Deezer API


## Installation

1. Clone or download the repo
1. ``npm i`` to install dependencies
1. ``npm run serve`` to view in browser



## Overview


![Albums page](/readme-images/albums-index.png)

Link to live site: https://vpaez.com/vep/


Project in collaboration with [Paul Aliu](https://github.com/SapienSumo) and [Emma Thompson](https://github.com/emma3333).

The brief was to create a website using a third-party API of our choice and React, working as a team and pair programming. It was the first pair programming project where our team of three programmers worked on the same computer.

After some research into different APIs, we decided to use Deezer's API, which is a music streaming service, because it provided us with sufficient information on the artists and albums (including album covers, number of tracks, audio samples for each track) and allowed us to do queries to search for albums by artist name.

## Process


### 1. Initial goal: a website to display Coldplay Albums

As a first instance, we created a very simple website with a page to display Coldplay's album covers. This was all done through fetching and displaying the data results for a query to [Deezer's API](https://developers.deezer.com/api/explorer).

```
https://api.deezer.com/search/artist?q=coldplay
```

![Coldplay Albums](/readme-images/coldplay-albums-index.png)


### 2. Implementing a search bar

We wanted the user to be able to search for an artist, and have all the albums related to that search displayed.

We implemented a search bar that uses the search value as a query string to make an axios request to Deezer's API. This was tricky because the search value was set in the Navbar Component and the axios request was being made from the Albums Index Component.


Once the user inputted a search value, the url path would change to include the search value as a query after /search/, so the request from the Albums Index Component, would be able to take that parameter and include it in the axios request.

```
<Route path="/search/:query" component={AlbumsIndex} />
```

```
handleSearch(e) {
    this.setState({ data: e.target.value })
  }

  handleSubmit(e) {
    e.preventDefault()

    this.props.history.push(`/search/${this.state.data}`)
  }
```

```
getData() {
  axios.get('https://cors-anywhere.herokuapp.com/api.deezer.com/search/album', {
    params: {
      q: this.props.match.params.query
    }
  })
    .then(res => {
      console.log(res.data)
      this.setState({ albums: res.data.data })
    })
}

```

### 3. Album Show Page
We then made an album show page where we displayed the album's cover, artist and duration. On image click, you could also see the tracklist.

![Album Show](/readme-images/album-show.png)

### 4. Extra features and styling

![Tracklist](/readme-images/tracklist.png)

As an extra feature we decided to add a small audio sample to each track, provided by Deezer's API.
We decided to have the audio tracklisting on the same page as the album to improve user experience.

We also included a featured artist section on the homepage.

![Featured](/readme-images/featured-artists.png)

### Challenges
It was one of my first times working with third-party APIs and it's sometimes difficult to understand some APIs' documentation. This contributed to our decision to use Deezer, as their documentation is simple and extremely user friendly.

### Wins

I learned a lot from pair programming as it allowed me to see other people's logic, and thought processes. We were all very new to programming and had different strengths, so we really complemented each other.


## Future features

To randomise the featured artists section each time the homepage is refreshed. A further improvement on this, would be to customise the artists based on the users preferences or search history. Since the finalisation of this project, I've had the opportunity to work with customised featured section on a different project: [Canvas](https://bit.ly/canvas-readme).  
