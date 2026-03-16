<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Random Joke Generator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 50px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            max-width: 700px;
            width: 100%;
        }

        h1 {
            text-align: center;
            color: #333;
            margin-bottom: 10px;
            font-size: 2.5em;
            background: linear-gradient(135deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .subtitle {
            text-align: center;
            color: #666;
            margin-bottom: 40px;
            font-size: 1em;
        }

        .joke-card {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 15px;
            padding: 40px;
            color: white;
            text-align: center;
            box-shadow: 0 10px 30px rgba(102, 126, 234, 0.3);
            margin-bottom: 30px;
            min-height: 200px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }

        .joke-type {
            font-size: 0.9em;
            opacity: 0.8;
            margin-bottom: 15px;
            text-transform: uppercase;
            letter-spacing: 2px;
            font-weight: 600;
        }

        .joke-text {
            font-size: 1.4em;
            font-weight: 500;
            line-height: 1.6;
            margin-bottom: 20px;
            min-height: 60px;
        }

        .joke-punchline {
            font-size: 1.3em;
            font-weight: 600;
            opacity: 0.9;
            margin-top: 20px;
            padding-top: 20px;
            border-top: 2px solid rgba(255, 255, 255, 0.3);
        }

        .loading {
            text-align: center;
            color: #667eea;
            font-size: 1.1em;
            font-weight: 600;
        }

        .spinner {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 4px solid #f3f3f3;
            border-top: 4px solid #667eea;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin-right: 10px;
            vertical-align: middle;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .controls {
            display: flex;
            gap: 15px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }

        button {
            flex: 1;
            padding: 15px 30px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            font-weight: 600;
            font-size: 1em;
            transition: all 0.3s ease;
            min-width: 150px;
        }

        button:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(102, 126, 234, 0.4);
        }

        button:active {
            transform: translateY(-1px);
        }

        button:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        .secondary-btn {
            background: #e0e0e0;
            color: #333;
        }

        .secondary-btn:hover {
            background: #d0d0d0;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
        }

        .category-select {
            flex: 1;
            padding: 15px;
            border: 2px solid #667eea;
            border-radius: 10px;
            font-size: 1em;
            cursor: pointer;
            background: white;
            color: #333;
            font-weight: 500;
            transition: all 0.3s ease;
            min-width: 200px;
        }

        .category-select:hover {
            border-color: #764ba2;
        }

        .category-select:focus {
            outline: none;
            border-color: #764ba2;
            box-shadow: 0 0 10px rgba(102, 126, 234, 0.2);
        }

        .stats {
            background: #f5f5f5;
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 20px;
            display: flex;
            justify-content: space-around;
            gap: 20px;
            flex-wrap: wrap;
        }

        .stat-item {
            text-align: center;
            color: #333;
        }

        .stat-label {
            font-size: 0.8em;
            color: #666;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 5px;
        }

        .stat-value {
            font-size: 1.8em;
            font-weight: bold;
            color: #667eea;
        }

        .copy-btn {
            background: #4CAF50;
            padding: 10px 20px;
            font-size: 0.9em;
            margin-top: 15px;
        }

        .copy-btn:hover {
            background: #45a049;
        }

        .error-message {
            background: #ffebee;
            color: #c62828;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            border-left: 4px solid #c62828;
        }

        .success-message {
            background: #e8f5e9;
            color: #2e7d32;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            border-left: 4px solid #2e7d32;
        }

        @media (max-width: 768px) {
            .container {
                padding: 30px;
            }

            h1 {
                font-size: 2em;
            }

            .joke-text {
                font-size: 1.2em;
            }

            .controls {
                flex-direction: column;
            }

            button, .category-select {
                width: 100%;
            }

            .stats {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>😂 Joke Generator</h1>
        <p class="subtitle">Get a laugh with random jokes from the internet</p>

        <div class="stats">
            <div class="stat-item">
                <div class="stat-label">Jokes Loaded</div>
                <div class="stat-value" id="jokeCount">0</div>
            </div>
            <div class="stat-item">
                <div class="stat-label">Favorites</div>
                <div class="stat-value" id="favoriteCount">0</div>
            </div>
        </div>

        <div id="messageContainer"></div>

        <div class="controls">
            <select id="categorySelect" class="category-select">
                <option value="">Random Joke</option>
                <option value="general">General</option>
                <option value="programming">Programming</option>
                <option value="knock-knock">Knock-Knock</option>
            </select>
            <button onclick="getJoke()">Get Joke</button>
            <button class="secondary-btn" onclick="toggleFavorite()">❤️ Favorite</button>
        </div>

        <div class="joke-card" id="jokeCard">
            <div class="loading">
                <span class="spinner"></span>
                Loading your first joke...
            </div>
        </div>

        <div class="controls">
            <button class="secondary-btn" onclick="copyJoke()">📋 Copy</button>
            <button class="secondary-btn" onclick="shareJoke()">📤 Share</button>
            <button class="secondary-btn" onclick="viewFavorites()">⭐ My Favorites</button>
        </div>
    </div>

    <script>
        let currentJoke = null;
        let jokeCount = 0;
        let favorites = JSON.parse(localStorage.getItem('favoriteJokes')) || [];
        let isFavorite = false;

        // Update stats
        function updateStats() {
            document.getElementById('jokeCount').textContent = jokeCount;
            document.getElementById('favoriteCount').textContent = favorites.length;
        }

        // Show message
        function showMessage(message, type = 'info') {
            const container = document.getElementById('messageContainer');
            const className = type === 'error' ? 'error-message' : type === 'success' ? 'success-message' : '';
            container.innerHTML = `<div class="${className}">${message}</div>`;
            setTimeout(() => {
                container.innerHTML = '';
            }, 3000);
        }

        // Fetch joke from API
        async function getJoke() {
            const jokeCard = document.getElementById('jokeCard');
            const category = document.getElementById('categorySelect').value;

            jokeCard.innerHTML = '<div class="loading"><span class="spinner"></span>Loading a joke...</div>';

            try {
                let url = 'https://official-joke-api.appspot.com/random_joke';

                if (category === 'programming') {
                    url = 'https://official-joke-api.appspot.com/jokes/programming/random';
                } else if (category === 'general') {
                    url = 'https://official-joke-api.appspot.com/jokes/general/random';
                } else if (category === 'knock-knock') {
                    url = 'https://official-joke-api.appspot.com/jokes/knock-knock/random';
                }

                const response = await fetch(url);
                if (!response.ok) throw new Error('Failed to fetch joke');

                let joke = await response.json();

                // Handle array response
                if (Array.isArray(joke)) {
                    joke = joke[0];
                }

                currentJoke = joke;
                jokeCount++;
                isFavorite = favorites.some(fav => 
                    fav.setup === joke.setup && fav.punchline === joke.punchline
                );

                displayJoke(joke);
                updateStats();
            } catch (error) {
                jokeCard.innerHTML = `
                    <div style="color: #d32f2f; font-size: 1.1em;">
                        😞 Oops! Failed to load joke.<br/>
                        Please check your internet connection and try again.
                    </div>
                `;
                showMessage('Error loading joke. Please try again!', 'error');
            }
        }

        // Display joke
        function displayJoke(joke) {
            const jokeCard = document.getElementById('jokeCard');
            const favoriteBtn = document.querySelector('.secondary-btn');
            const heartIcon = isFavorite ? '❤️' : '🤍';

            let jokeHTML = `
                <div class="joke-type">${joke.type || 'General Joke'}</div>
                <div class="joke-text">${joke.setup}</div>
            `;

            if (joke.punchline) {
                jokeHTML += `<div class="joke-punchline">${joke.punchline}</div>`;
            } else if (joke.joke) {
                jokeHTML += `<div class="joke-punchline">${joke.joke}</div>`;
            }

            jokeCard.innerHTML = jokeHTML;
            document.querySelectorAll('.secondary-btn')[1].textContent = `${heartIcon} Favorite`;
        }

        // Toggle favorite
        function toggleFavorite() {
            if (!currentJoke) {
                showMessage('Get a joke first!', 'error');
                return;
            }

            const jokeToFav = {
                setup: currentJoke.setup,
                punchline: currentJoke.punchline || currentJoke.joke,
                type: currentJoke.type
            };

            const index = favorites.findIndex(fav =>
                fav.setup === jokeToFav.setup && fav.punchline === jokeToFav.punchline
            );

            if (index > -1) {
                favorites.splice(index, 1);
                isFavorite = false;
                showMessage('Removed from favorites', 'success');
            } else {
                favorites.push(jokeToFav);
                isFavorite = true;
                showMessage('Added to favorites! ⭐', 'success');
            }

            localStorage.setItem('favoriteJokes', JSON.stringify(favorites));
            updateStats();
            displayJoke(currentJoke);
        }

        // Copy joke
        function copyJoke() {
            if (!currentJoke) {
                showMessage('Get a joke first!', 'error');
                return;
            }

            const jokeText = `${currentJoke.setup}\n\n${currentJoke.punchline || currentJoke.joke}`;
            navigator.clipboard.writeText(jokeText).then(() => {
                showMessage('Joke copied to clipboard! 📋', 'success');
            }).catch(() => {
                showMessage('Failed to copy joke', 'error');
            });
        }

        // Share joke
        function shareJoke() {
            if (!currentJoke) {
                showMessage('Get a joke first!', 'error');
                return;
            }

            const jokeText = `${currentJoke.setup}\n\n${currentJoke.punchline || currentJoke.joke}`;

            if (navigator.share) {
                navigator.share({
                    title: 'Check out this joke!',
                    text: jokeText
                }).catch(() => {});
            } else {
                showMessage('Share feature not supported on this browser', 'error');
            }
        }

        // View favorites
        function viewFavorites() {
            if (favorites.length === 0) {
                showMessage('No favorites yet! Get some jokes and add them to favorites.', 'error');
                return;
            }

            const jokeCard = document.getElementById('jokeCard');
            let favHTML = '<div style="text-align: left;"><h3 style="margin-bottom: 15px; color: #667eea;">⭐ Your Favorites</h3>';

            favorites.forEach((fav, index) => {
                favHTML += `
                    <div style="background: rgba(102, 126, 234, 0.1); padding: 15px; border-radius: 8px; margin-bottom: 10px; cursor: pointer;" onclick="displayFavorite(${index})">
                        <strong>${index + 1}.</strong> ${fav.setup.substring(0, 50)}...
                    </div>
                `;
            });

            favHTML += '</div>';
            jokeCard.innerHTML = favHTML;
        }

        // Display favorite joke
        function displayFavorite(index) {
            const fav = favorites[index];
            currentJoke = fav;
            isFavorite = true;
            displayJoke(fav);
        }

        // Initialize app
        updateStats();
        getJoke();
    </script>
</body>
</html>
