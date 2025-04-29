# Movie Recommendation System

A simple, standalone movie recommendation system built with HTML, JavaScript, and Tailwind CSS. This application demonstrates core recommendation algorithms without requiring any server setup, database, or build process.

## 🎬 Features

- **Content-based filtering algorithm** that recommends movies based on genre preferences
- **Simple, intuitive UI** for discovering and rating movies
- **Genre filtering** to browse movies by category
- **Real-time recommendations** that update as you like movies
- **Match percentage** showing how closely a recommendation matches your preferences
- **Fully client-side** implementation with no server dependencies

## 🚀 Quick Start

1. **Download the HTML file:**
   - Clone this repository: `git clone https://github.com/husal90/movie-recommendation-system.git`
   - Or download the `index.html` file directly

2. **Open the file:**
   - Double-click the HTML file to open it in your default browser
   - That's it! No installation, no setup

## 💡 How It Works

The recommendation system uses a hybrid approach:

1. **Content-based filtering:**
   - Analyzes the genres of movies you like
   - Weighs genres based on frequency in your liked movies
   - Finds similar movies that match your genre preferences

2. **Quality-based scoring:**
   - Considers movie ratings as a quality factor
   - Combines with genre similarity for better recommendations

3. **Weighted algorithm:**
   - Genre similarity: 70% of the recommendation score
   - Movie rating: 30% of the recommendation score

## 🧠 Recommendation Algorithm

```javascript
// Calculate a score for each movie based on genre overlap and rating
const scoredMovies = movieDatabase
  .filter(movie => !likedMovies.some(m => m.id === movie.id))
  .map(movie => {
    // Genre similarity score
    let genreScore = movie.genres.reduce((score, genre) => {
      return score + (likedGenres[genre] || 0);
    }, 0) / movie.genres.length;
    
    // Normalize genre score (0-1)
    const maxGenreScore = Math.max(...Object.values(likedGenres));
    genreScore = genreScore / maxGenreScore;
    
    // Rating score (normalized to 0-1)
    const ratingScore = movie.rating / 10;
    
    // Combined score (70% genre similarity, 30% rating)
    const totalScore = (genreScore * 0.7) + (ratingScore * 0.3);
    
    return {
      ...movie,
      score: totalScore
    };
  });
```

## 🛠️ Technologies Used

- **HTML5** - Structure
- **JavaScript** - Logic and interactivity
- **Tailwind CSS** - Styling (via CDN)
- **Lodash** - Utility functions for data manipulation (via CDN)

## 📚 Movie Database

The system includes a curated database of 20 popular movies with their:
- Titles
- Release years
- Genres
- IMDb ratings

You can easily extend the database by modifying the `movieDatabase` array in the JavaScript code.

## 🔍 Future Enhancements

Possible improvements to explore:
- User accounts and persistent storage with localStorage
- More sophisticated collaborative filtering
- Additional movie metadata (directors, actors, etc.)
- Support for user ratings instead of just likes
- Expanded movie database

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👤 Author

- GitHub: [@husal90](https://github.com/husal90)

## 🙏 Acknowledgments

- Movie data inspired by IMDb top movies
- Built as a demonstration of recommendation systems in client-side JavaScript
