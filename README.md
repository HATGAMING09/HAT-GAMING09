<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HAT GAMING09 - Game & News Hub</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #1a1a1a;
            color: white;
            margin: 0;
            padding: 20px;
        }
        h1 {
            color: #ffcc00;
        }
        h2 {
            color: #ff5733;
        }
        #news-container, #games-container {
            margin-top: 20px;
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
        }
        .card {
            border: 1px solid #444;
            margin: 10px;
            padding: 10px;
            width: 300px;
            background-color: #222;
            border-radius: 5px;
            text-align: left;
        }
        img {
            width: 100%;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <h1>Welcome to HAT GAMING09</h1>
    <p>Your ultimate hub for gaming news and trending games!</p>

    <h2>🔥 Latest News</h2>
    <div id="news-container"></div>

    <h2>🎮 Trending Games</h2>
    <div id="games-container"></div>

    <!-- Firebase SDK (ES Module) -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.4.0/firebase-app.js";
        import { getDatabase, ref, set, get, child } from "https://www.gstatic.com/firebasejs/11.4.0/firebase-database.js";
        
        // 🔥 Firebase Configuration
        const firebaseConfig = {
            apiKey: "AlzaSyB9HeD8qfokjCwBvX__W8FsRmEu4w707-k",
            authDomain: "hat-gaming09.firebaseapp.com",
            databaseURL: "https://hat-gaming09-default-rtdb.asia-southeast1.firebasedatabase.app",
            projectId: "hat-gaming09",
            storageBucket: "hat-gaming09.appspot.com",
            messagingSenderId: "957587631587",
            appId: "1:957587631587:web:2f3009df500701b041c4d6",
            measurementId: "G-K8BPD7CBFZ"
        };

        // Initialize Firebase
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        // 🔥 Function to Fetch News
        async function fetchNews() {
            const apiKey = "63a4e1dcaedd44eeb43dcbc48c8a6887";
            const url = `https://newsapi.org/v2/top-headlines?country=us&apiKey=${apiKey}`;
            try {
                const response = await fetch(url);
                const data = await response.json();
                const newsContainer = document.getElementById("news-container");
                newsContainer.innerHTML = "";
                data.articles.slice(0, 5).forEach(article => {
                    const div = document.createElement("div");
                    div.classList.add("card");
                    div.innerHTML = `
                        <h3>${article.title}</h3>
                        <img src="${article.urlToImage || 'https://via.placeholder.com/300'}" alt="News Image">
                        <p>${article.description || "No description available"}</p>
                        <a href="${article.url}" target="_blank">Read More</a>
                    `;
                    newsContainer.appendChild(div);
                });
            } catch (error) {
                console.error("Error fetching news:", error);
            }
        }

        // 🎮 Function to Fetch Games
        async function fetchGames() {
            const apiKey = "317b7cbad7c3457d909d74ed33009004";
            const url = `https://api.rawg.io/api/games?key=${apiKey}`;
            try {
                const response = await fetch(url);
                const data = await response.json();
                const gamesContainer = document.getElementById("games-container");
                gamesContainer.innerHTML = "";
                data.results.slice(0, 5).forEach(game => {
                    const div = document.createElement("div");
                    div.classList.add("card");
                    div.innerHTML = `
                        <h3>${game.name}</h3>
                        <img src="${game.background_image}" alt="Game Image">
                    `;
                    gamesContainer.appendChild(div);
                });
            } catch (error) {
                console.error("Error fetching games:", error);
            }
        }

        // Load News and Games on Page Load
        fetchNews();
        fetchGames();
    </script>
</body>
</html>
