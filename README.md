# TicTacToe

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Criss-Cross (Tic-Tac-Toe) Game</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #1e272e;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            overflow: hidden;
        }

        h1 {
            color: #fff;
            font-size: 2.5rem;
            margin-bottom: 20px;
        }

        .container {
            text-align: center;
            animation: fadeIn 0.5s ease-in-out;
        }

        .board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            grid-gap: 10px;
            margin: 20px auto;
        }

        .cell {
            background-color: #f7f1e3;
            border: 2px solid #57606f;
            font-size: 2rem;
            font-weight: bold;
            color: #2f3542;
            display: flex;
            justify-content: center;
            align-items: center;
            width: 100px;
            height: 100px;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s ease;
        }

        .cell:hover {
            background-color: #ff6b81;
            transform: scale(1.1);
        }

        #message {
            font-size: 1.5rem;
            color: #f1f2f6;
            margin-bottom: 10px;
        }

        .button {
            background-color: #ff4757;
            color: white;
            border: none;
            padding: 10px 20px;
            font-size: 1rem;
            cursor: pointer;
            border-radius: 5px;
            margin: 10px;
            transition: background-color 0.3s ease, transform 0.2s ease;
        }

        .button:hover {
            background-color: #e74c3c;
            transform: scale(1.05);
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }
    </style>
</head>
<body>

    <!-- Welcome Page -->
    <div id="welcome-page" class="container">
        <h1>Welcome to Criss-Cross (Tic-Tac-Toe)</h1>
        <button class="button" onclick="showGamePage()">Start Game</button>
    </div>

    <!-- Game Page -->
    <div id="game-page" class="container" style="display:none;">
        <h1>Tic-Tac-Toe</h1>
        <div id="message">Player X's turn</div>
        <div class="board">
            <div class="cell" onclick="handleClick(0)"></div>
            <div class="cell" onclick="handleClick(1)"></div>
            <div class="cell" onclick="handleClick(2)"></div>
            <div class="cell" onclick="handleClick(3)"></div>
            <div class="cell" onclick="handleClick(4)"></div>
            <div class="cell" onclick="handleClick(5)"></div>
            <div class="cell" onclick="handleClick(6)"></div>
            <div class="cell" onclick="handleClick(7)"></div>
            <div class="cell" onclick="handleClick(8)"></div>
        </div>
        <button class="button" onclick="resetGame()">Reset Game</button>
        <button class="button" onclick="goBack()">Go Back</button>
    </div>

    <!-- Game Over Page -->
    <div id="game-over-page" class="container" style="display:none;">
        <h1 id="winner-message"></h1>
        <button class="button" onclick="restartGame()">Play Again</button>
        <button class="button" onclick="goBack()">Go Back</button>
    </div>

    <script>
        let board = ["", "", "", "", "", "", "", "", ""];
        let currentPlayer = "X";
        let isGameOver = false;

        // Function to handle cell clicks
        function handleClick(index) {
            if (board[index] === "" && !isGameOver) {
                board[index] = currentPlayer;
                document.getElementsByClassName("cell")[index].textContent = currentPlayer;
                document.getElementsByClassName("cell")[index].style.color = currentPlayer === 'X' ? '#ff4757' : '#1e90ff';

                if (checkWinner()) {
                    document.getElementById("message").textContent = "Player " + currentPlayer + " wins!";
                    isGameOver = true;
                    showGameOverPage(currentPlayer + " Wins!");
                } else if (board.every(cell => cell !== "")) {
                    document.getElementById("message").textContent = "It's a draw!";
                    showGameOverPage("It's a Draw!");
                    isGameOver = true;
                } else {
                    currentPlayer = currentPlayer === "X" ? "O" : "X";
                    document.getElementById("message").textContent = "Player " + currentPlayer + "'s turn";
                }
            }
        }

        // Function to check if the current player has won
        function checkWinner() {
            const winningCombinations = [
                [0, 1, 2],
                [3, 4, 5],
                [6, 7, 8],
                [0, 3, 6],
                [1, 4, 7],
                [2, 5, 8],
                [0, 4, 8],
                [2, 4, 6]
            ];
            return winningCombinations.some(combination => {
                return combination.every(index => board[index] === currentPlayer);
            });
        }

        // Function to reset the game
        function resetGame() {
            board = ["", "", "", "", "", "", "", "", ""];
            currentPlayer = "X";
            isGameOver = false;
            document.getElementById("message").textContent = "Player X's turn";
            let cells = document.getElementsByClassName("cell");
            for (let cell of cells) {
                cell.textContent = "";
            }
        }

        // Function to show the game page
        function showGamePage() {
            document.getElementById("welcome-page").style.display = "none";
            document.getElementById("game-page").style.display = "block";
        }

        // Function to show the game over page
        function showGameOverPage(winnerMessage) {
            document.getElementById("game-page").style.display = "none";
            document.getElementById("game-over-page").style.display = "block";
            document.getElementById("winner-message").textContent = winnerMessage;
        }

        // Function to restart the game
        function restartGame() {
            resetGame();
            document.getElementById("game-over-page").style.display = "none";
            document.getElementById("game-page").style.display = "block";
        }

        // Function to go back to the welcome page
        function goBack() {
            resetGame();
            document.getElementById("game-page").style.display = "none";
            document.getElementById("game-over-page").style.display = "none";
            document.getElementById("welcome-page").style.display = "block";
        }
    </script>
</body>
</html>
