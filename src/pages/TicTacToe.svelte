<script>
    let board = Array(9).fill(null);
    let currentPlayer = 'X';
    let winner = null;
  
    const checkWinner = () => {
      const winningCombinations = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];
      for (let combo of winningCombinations) {
        const [a, b, c] = combo;
        if (board[a] && board[a] === board[b] && board[a] === board[c]) {
          return board[a];
        }
      }
      return null;
    };
  
    const handleClick = (index) => {
      if (!board[index] && !winner) {
        board[index] = currentPlayer;
        winner = checkWinner();
        currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
      }
    };
  
    const resetGame = () => {
      board = Array(9).fill(null);
      currentPlayer = 'X';
      winner = null;
    };
  </script>
  
  <h2>Križec-Krožec</h2>
  <p>{winner ? `Zmagovalec je ${winner}` : `Na potezi je: ${currentPlayer}`}</p>
  
  <div class="board">
    {#each board as cell, index}
      <div class="cell" on:click={() => handleClick(index)}>
        {cell}
      </div>
    {/each}
  </div>
  
  <button on:click={resetGame}>Ponastavi igro</button>
  
  <style>
    h2 {
      text-align: center;
      color: #007bff;
    }
  
    .board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-gap: 5px;
      justify-content: center;
      margin: 20px auto;
    }
  
    .cell {
      width: 100px;
      height: 100px;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 2rem;
      border: 1px solid #333;
      cursor: pointer;
    }
  
    .cell:hover {
      background-color: #f0f0f0;
    }
  
    button {
      display: block;
      margin: 20px auto;
      padding: 10px 20px;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 5px;
      font-size: 1rem;
      cursor: pointer;
    }
  
    button:hover {
      background-color: #0056b3;
    }
  </style>
  