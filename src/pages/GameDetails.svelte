<script>
  import { onMount } from 'svelte';
  import { cart } from '../stores/cart';

  import catanImage from "../assets/CATAN.jpg";
  import monopolyImage from "../assets/multicolorhasbro-games-druzabna-igra-za-2-ali-vec-igralcev-1.jpg";
  import dixitImage from "../assets/dixitdisney.jpg";

  const gameList = [
    { id: 1, name: "Naseljenci otoka Catan", description: "Strategija in trgovanje med igralci.", image: catanImage, pricePerDay: 2 },
    { id: 2, name: "Monopoly", description: "Klasična igra za trgovanje z nepremičninami.", image: monopolyImage, pricePerDay: 1.5 },
    { id: 3, name: "Dixit", description: "Kreativna pripovedna igra za vse starosti.", image: dixitImage, pricePerDay: 1 },
  ];

  export let params;
  let game;
  let selectedDays = 1;
  let showConfirmation = false; // Za obvestilo

  const addToCart = () => {
    const gameWithDetails = { ...game, days: selectedDays, totalPrice: selectedDays * game.pricePerDay };
    cart.update((items) => [...items, gameWithDetails]);
    showConfirmation = true;
    setTimeout(() => (showConfirmation = false), 2000); // Obvestilo izgine po 2 sekundah
  };

  onMount(() => {
    const gameId = params.id;
    game = gameList.find((g) => g.id == Number(gameId));
  });
</script>

{#if game}
  <h1>{game.name}</h1>
  <img src={game.image} alt={game.name} />
  <p>{game.description}</p>
  <p>Cena na dan: {game.pricePerDay} €</p>
  <label>
    Število dni za izposojo:
    <input type="number" min="1" bind:value={selectedDays} />
  </label>
  <button on:click={addToCart}>Dodaj v košarico</button>
  {#if showConfirmation}
    <p class="confirmation">Igra je bila dodana v košarico!</p>
  {/if}
  <button on:click={() => (window.location.href = "/")}>Nazaj na seznam</button>
{:else}
  <p>Igra ni najdena.</p>
{/if}

<style>
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


  label {
    display: block;
    text-align: center;
    margin: 1rem 0;
  }
  input {
    display: block;
    margin: 0.5rem auto;
    padding: 0.5rem;
    font-size: 1rem;
    width: 100px;
  }

  h1 {
    text-align: center;
    color: #007bff;
  }
  img {
    display: block;
    margin: 1rem auto;
    max-width: 300px;
    border-radius: 8px;
  }
  p {
    text-align: center;
    color: #333;
  }
  button {
    display: block;
    margin: 1rem auto;
    padding: 0.5rem 1rem;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  button:hover {
    background-color: #0056b3;
  }
  .confirmation {
    text-align: center;
    color: green;
    margin-top: 1rem;
    font-weight: bold;
  }

  @media (max-width: 768px) {
  h1 {
    font-size: 1.5rem;
  }

  img {
    max-width: 250px;
  }

  p {
    font-size: 0.9rem;
  }

  button {
    padding: 0.4rem 0.8rem;
    font-size: 0.9rem;
  }
}

@media (max-width: 480px) {
  h1 {
    font-size: 1.2rem;
  }

  img {
    max-width: 200px;
  }

  button {
    font-size: 0.8rem;
    padding: 0.3rem 0.6rem;
  }
}
</style>
