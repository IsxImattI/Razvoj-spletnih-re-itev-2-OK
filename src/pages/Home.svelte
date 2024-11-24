<script>
  import catanImage from "../assets/CATAN.jpg";
  import monopolyImage from "../assets/multicolorhasbro-games-druzabna-igra-za-2-ali-vec-igralcev-1.jpg";
  import dixitImage from "../assets/dixitdisney.jpg";
  import { cart } from '../stores/cart';
  

  let games = [
    { id: 1, name: "Naseljenci otoka Catan", category: "Strategija", image: catanImage, pricePerDay: 2 },
    { id: 2, name: "Monopoly", category: "Družinske igre", image: monopolyImage, pricePerDay: 1.5 },
    { id: 3, name: "Dixit", category: "Družinske igre", image: dixitImage, pricePerDay: 1 },
  ];

  let selectedCategory = "Vse";
  let selectedDays = 1;
  let showConfirmation = false; // Za obvestila

  const filteredGames = () => {
    return selectedCategory === "Vse"
      ? games
      : games.filter((game) => game.category === selectedCategory);
  };

  const addToCart = (game) => {
    const gameWithDetails = { ...game, days: selectedDays, totalPrice: selectedDays * game.pricePerDay };
    cart.update((items) => [...items, gameWithDetails]);
    showConfirmation = true;
    setTimeout(() => (showConfirmation = false), 2000); // Skrije obvestilo po 2 sekundah
  };
</script>

<h2>Seznam družabnih iger</h2>

<!-- Obvestilo za košarico -->
{#if showConfirmation}
  <p class="confirmation">Igra je bila dodana v košarico!</p>
{/if}

<div class="filters">
  <label>
    Filtriraj po kategoriji:
    <select bind:value={selectedCategory}>
      <option value="Vse">Vse</option>
      <option value="Strategija">Strategija</option>
      <option value="Družinske igre">Družinske igre</option>
    </select>
  </label>
  <label>
    Število dni za izposojo:
    <input type="number" min="1" bind:value={selectedDays} />
  </label>
</div>

<div class="games">
  {#each filteredGames() as game}
    <div class="card">
      <img src={game.image} alt={game.name} />
      <h3>{game.name}</h3>
      <p>Kategorija: {game.category}</p>
      <p>Cena na dan: {game.pricePerDay} €</p>
      <button on:click={() => addToCart(game)}>Dodaj v košarico</button>
      <button on:click={() => (window.location.href = `/game/${game.id}`)}>Več informacij</button>
    </div>
  {/each}
</div>

<style>
  .games {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); /* Več prostora za slike */
    gap: 1.5rem;
    padding: 2rem;
    max-width: 1200px;
    margin: 0 auto; /* Centriranje vsebine */
  }
  
  .card {
    background-color: #ffffff;
    color: #333;
    padding: 1.5rem;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s, box-shadow 0.3s;
    text-align: center; /* Centriranje besedila */
  }
  
  .card:hover {
    transform: scale(1.03);
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
  }
  
  .card img {
    border-radius: 8px;
    max-width: 100%;
    max-height: 180px; /* Omejitev višine slik */
    object-fit: cover; /* Prilagoditev velikosti slike */
    margin-bottom: 1rem;
  }
  
  .card h3 {
    font-size: 1.2rem;
    color: #007bff;
    margin-bottom: 0.5rem;
  }
  
  .card p {
    color: #555;
    margin-bottom: 1rem;
  }
  
  .card button {
    margin: 0.5rem 0;
    background-color: #007bff;
    color: white;
    border: none;
    padding: 0.5rem 1rem;
    font-size: 1rem;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .card button:hover {
    background-color: #0056b3;
  }
  
  .filters {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 1.5rem auto;
    max-width: 800px; /* Centriranje filtrov */
  }
  
  .filters label {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    font-size: 1rem;
    color: #333;
  }
  
  h2 {
    text-align: center;
    font-size: 2rem;
    color: #333;
    margin-bottom: 1.5rem;
  }

  .confirmation {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #28a745;
  color: white;
  padding: 1rem 2rem;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  z-index: 1000;
  animation: fadeInOut 2s ease-in-out;
}

@keyframes fadeInOut {
  0% {
    opacity: 0;
    transform: translate(-50%, -60%);
  }
  20%,
  80% {
    opacity: 1;
    transform: translate(-50%, -50%);
  }
  100% {
    opacity: 0;
    transform: translate(-50%, -60%);
  }
}

@media (max-width: 768px) {
  .games {
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
    padding: 1rem;
  }

  .card {
    padding: 1rem;
  }

  .card h3 {
    font-size: 1rem;
  }

  .card p {
    font-size: 0.9rem;
  }

  .card button {
    padding: 0.4rem 0.8rem;
    font-size: 0.8rem;
  }
}

@media (max-width: 480px) {
  .games {
    grid-template-columns: 1fr;
  }

  .card img {
    max-width: 80%;
  }
}
  </style>
  
