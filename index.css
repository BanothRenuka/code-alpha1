<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hangman Game</title>
    <style>
        * {
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #2c3e50;
            color: #ecf0f1;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
        }
        
        .container {
            background-color: #34495e;
            border-radius: 10px;
            padding: 30px;
            width: 100%;
            max-width: 700px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.5);
        }
        
        h1 {
            text-align: center;
            color: #f1c40f;
            margin-top: 0;
            font-size: 2.5rem;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }
        
        .game-area {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        
        .game-info {
            display: flex;
            justify-content: space-between;
            background-color: #2c3e50;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 10px;
        }
        
        .hangman-display {
            text-align: center;
            font-size: 1.2rem;
            background-color: #2c3e50;
            padding: 15px;
            border-radius: 8px;
            min-height: 80px;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }
        
        .word-display {
            text-align: center;
            font-size: 2.5rem;
            letter-spacing: 10px;
            margin: 20px 0;
            font-weight: bold;
            color: #3498db;
            min-height: 60px;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .incorrect-guesses {
            text-align: center;
            font-size: 1.3rem;
            color: #e74c3c;
            min-height: 30px;
            margin-bottom: 10px;
        }
        
        .input-area {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-bottom: 20px;
        }
        
        #letter-input {
            width: 60px;
            height: 60px;
            text-align: center;
            font-size: 1.8rem;
            font-weight: bold;
            text-transform: uppercase;
            border: none;
            border-radius: 5px;
            background-color: #ecf0f1;
            color: #2c3e50;
        }
        
        .buttons {
            display: flex;
            justify-content: center;
            gap: 15px;
        }
        
        button {
            padding: 12px 25px;
            font-size: 1.1rem;
            font-weight: bold;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        #guess-btn {
            background-color: #27ae60;
            color: white;
        }
        
        #guess-btn:hover {
            background-color: #229954;
        }
        
        #guess-btn:disabled {
            background-color: #7f8c8d;
            cursor: not-allowed;
        }
        
        #restart-btn {
            background-color: #e67e22;
            color: white;
        }
        
        #restart-btn:hover {
            background-color: #d35400;
        }
        
        .message {
            text-align: center;
            font-size: 1.5rem;
            font-weight: bold;
            padding: 15px;
            border-radius: 8px;
            margin-top: 10px;
            min-height: 60px;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .win {
            background-color: rgba(46, 204, 113, 0.3);
            color: #2ecc71;
        }
        
        .lose {
            background-color: rgba(231, 76, 60, 0.3);
            color: #e74c3c;
        }
        
        .instructions {
            background-color: #2c3e50;
            padding: 15px;
            border-radius: 8px;
            margin-top: 20px;
            font-size: 1rem;
            line-height: 1.5;
        }
        
        @media (max-width: 600px) {
            .container {
                padding: 15px;
            }
            
            h1 {
                font-size: 2rem;
            }
            
            .word-display {
                font-size: 1.8rem;
                letter-spacing: 8px;
            }
            
            .buttons {
                flex-direction: column;
            }
            
            button {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🎮 Hangman Game</h1>
        
        <div class="game-area">
            <div class="game-info">
                <div>Remaining Guesses: <span id="remaining-guesses">6</span></div>
                <div>Words in Game: <span id="word-count">5</span></div>
            </div>
            
            <div class="hangman-display" id="hangman-status">
                Guess the word by entering letters one at a time!
            </div>
            
            <div class="word-display" id="word-display"></div>
            
            <div class="incorrect-guesses" id="incorrect-letters">
                Incorrect letters: None yet
            </div>
            
            <div class="input-area">
                <input type="text" id="letter-input" maxlength="1" placeholder="?">
            </div>
            
            <div class="buttons">
                <button id="guess-btn">Guess Letter</button>
                <button id="restart-btn">New Game</button>
            </div>
            
            <div class="message" id="message"></div>
            
            <div class="instructions">
                <h3>How to Play:</h3>
                <p>1. Try to guess the hidden word by entering letters one at a time.</p>
                <p>2. You have 6 incorrect guesses before you lose the game.</p>
                <p>3. Correct guesses will reveal the letter in the word.</p>
                <p>4. Win by guessing all letters in the word before running out of guesses.</p>
            </div>
        </div>
    </div>

    <script>
        // Predefined word list
        const wordList = ["PYTHON", "JAVASCRIPT", "HANGMAN", "PROGRAMMING", "COMPUTER"];
        
        // Game state variables
        let currentWord = "";
        let displayWord = [];
        let incorrectGuesses = [];
        let remainingGuesses = 6;
        let gameOver = false;
        let guessedLetters = [];
        
        // DOM elements
        const wordDisplayEl = document.getElementById("word-display");
        const incorrectLettersEl = document.getElementById("incorrect-letters");
        const remainingGuessesEl = document.getElementById("remaining-guesses");
        const letterInputEl = document.getElementById("letter-input");
        const guessBtn = document.getElementById("guess-btn");
        const restartBtn = document.getElementById("restart-btn");
        const messageEl = document.getElementById("message");
        const hangmanStatusEl = document.getElementById("hangman-status");
        const wordCountEl = document.getElementById("word-count");
        
        // Initialize game
        function initGame() {
            // Reset game state
            currentWord = wordList[Math.floor(Math.random() * wordList.length)];
            displayWord = Array(currentWord.length).fill("_");
            incorrectGuesses = [];
            guessedLetters = [];
            remainingGuesses = 6;
            gameOver = false;
            
            // Update UI
            updateWordDisplay();
            updateIncorrectLetters();
            updateRemainingGuesses();
            updateHangmanStatus();
            clearMessage();
            wordCountEl.textContent = wordList.length;
            
            // Enable input and button
            letterInputEl.disabled = false;
            guessBtn.disabled = false;
            letterInputEl.value = "";
            letterInputEl.focus();
        }
        
        // Update the word display with underscores and correctly guessed letters
        function updateWordDisplay() {
            wordDisplayEl.textContent = displayWord.join(" ");
        }
        
        // Update the incorrect letters display
        function updateIncorrectLetters() {
            if (incorrectGuesses.length === 0) {
                incorrectLettersEl.textContent = "Incorrect letters: None yet";
            } else {
                incorrectLettersEl.textContent = `Incorrect letters: ${incorrectGuesses.join(", ")}`;
            }
        }
        
        // Update the remaining guesses display
        function updateRemainingGuesses() {
            remainingGuessesEl.textContent = remainingGuesses;
        }
        
        // Update the hangman status message
        function updateHangmanStatus() {
            const statusMessages = [
                "No wrong guesses yet. The hangman is safe!",
                "One wrong guess. Head drawn.",
                "Two wrong guesses. Body drawn.",
                "Three wrong guesses. One arm drawn.",
                "Four wrong guesses. Both arms drawn.",
                "Five wrong guesses. One leg drawn.",
                "Six wrong guesses. Hangman complete! Game over."
            ];
            
            const wrongCount = 6 - remainingGuesses;
            hangmanStatusEl.textContent = statusMessages[wrongCount];
        }
        
        // Display a message to the player
        function displayMessage(text, isWin) {
            messageEl.textContent = text;
            messageEl.className = "message";
            
            if (isWin !== undefined) {
                messageEl.classList.add(isWin ? "win" : "lose");
            }
        }
        
        // Clear the message display
        function clearMessage() {
            messageEl.textContent = "";
            messageEl.className = "message";
        }
        
        // Process a letter guess
        function processGuess(letter) {
            // Check if game is over
            if (gameOver) {
                displayMessage("Game over! Please start a new game.", false);
                return;
            }
            
            // Validate input
            if (!letter || letter.length !== 1) {
                displayMessage("Please enter a single letter.", false);
                return;
            }
            
            letter = letter.toUpperCase();
            
            // Check if letter is A-Z
            if (letter < 'A' || letter > 'Z') {
                displayMessage("Please enter a letter from A to Z.", false);
                return;
            }
            
            // Check if letter was already guessed
            if (guessedLetters.includes(letter)) {
                displayMessage(`You already guessed "${letter}". Try a different letter.`, false);
                return;
            }
            
            // Add to guessed letters
            guessedLetters.push(letter);
            
            // Check if letter is in the word
            if (currentWord.includes(letter)) {
                // Correct guess - reveal the letter in the word
                for (let i = 0; i < currentWord.length; i++) {
                    if (currentWord[i] === letter) {
                        displayWord[i] = letter;
                    }
                }
                
                updateWordDisplay();
                displayMessage(`Good guess! "${letter}" is in the word.`);
                
                // Check if player won
                if (!displayWord.includes("_")) {
                    gameOver = true;
                    displayMessage(`Congratulations! You won! The word was "${currentWord}".`, true);
                    letterInputEl.disabled = true;
                    guessBtn.disabled = true;
                }
            } else {
                // Incorrect guess
                incorrectGuesses.push(letter);
                remainingGuesses--;
                
                updateIncorrectLetters();
                updateRemainingGuesses();
                updateHangmanStatus();
                
                displayMessage(`Sorry, "${letter}" is not in the word.`);
                
                // Check if player lost
                if (remainingGuesses <= 0) {
                    gameOver = true;
                    displayMessage(`Game over! The word was "${currentWord}". Try again!`, false);
                    letterInputEl.disabled = true;
                    guessBtn.disabled = true;
                }
            }
            
            // Clear the input field
            letterInputEl.value = "";
            letterInputEl.focus();
        }
        
        // Event listeners
        guessBtn.addEventListener("click", function() {
            const letter = letterInputEl.value.trim();
            processGuess(letter);
        });
        
        restartBtn.addEventListener("click", initGame);
        
        // Allow pressing Enter to guess
        letterInputEl.addEventListener("keyup", function(event) {
            if (event.key === "Enter") {
                const letter = letterInputEl.value.trim();
                processGuess(letter);
            }
        });
        
        // Only allow letters in the input field
        letterInputEl.addEventListener("input", function() {
            this.value = this.value.replace(/[^a-zA-Z]/g, '');
        });
        
        // Initialize the game when page loads
        document.addEventListener("DOMContentLoaded", initGame);
    </script>
</body>
</html>