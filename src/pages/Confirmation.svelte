<script>
  import { cart } from "../stores/cart";

  let totalPrice = 0;
  let showConfirmation = false; // Za prikaz obvestila

  cart.subscribe((items) => {
    totalPrice = items.reduce((sum, item) => sum + item.totalPrice, 0);
  });

  const completeOrder = () => {
    if ($cart.length > 0) {
      showConfirmation = true; // Pokaži obvestilo
      cart.set([]); // Počisti košarico
      setTimeout(() => {
        showConfirmation = false; // Skrij obvestilo po 3 sekundah
      }, 3000);
    }
  };
</script>

<h2>Povzetek naročila</h2>

<!-- Obvestilo o uspešnem zaključku naročila -->
{#if showConfirmation}
  <p class="confirmation">Vaše naročilo je bilo uspešno zaključeno!</p>
{/if}

{#if $cart.length > 0}
  <ul class="summary">
    {#each $cart as item}
      <li>
        <img src={item.image} alt={item.name} />
        <div>
          <h3>{item.name}</h3>
          <p>Število dni: {item.days}</p>
          <p>Skupna cena: {item.totalPrice.toFixed(2)} €</p>
        </div>
      </li>
    {/each}
  </ul>
  <p class="total-price">Skupna cena vseh iger: {totalPrice.toFixed(2)} €</p>
  <button on:click={completeOrder}>Zaključi naročilo</button>
{:else}
  <p>Vaša košarica je prazna.</p>
{/if}

<style>
  h2 {
    text-align: center;
    color: #007bff;
  }
  .summary {
    list-style: none;
    padding: 0;
    margin: 2rem auto;
    max-width: 600px;
  }
  .summary li {
    display: flex;
    gap: 1rem;
    padding: 1rem;
    border-bottom: 1px solid #ddd;
  }
  .summary img {
    width: 100px;
    height: auto;
    border-radius: 8px;
  }
  .summary div {
    flex-grow: 1;
  }
  .summary h3 {
    margin: 0;
    color: #333;
  }
  .summary p {
    margin: 0.5rem 0;
    color: #666;
  }
  .total-price {
    text-align: center;
    font-size: 1.2rem;
    font-weight: bold;
    color: #333;
    margin: 1rem 0;
  }
  button {
    display: block;
    margin: 2rem auto;
    padding: 0.5rem 1rem;
    background-color: #28a745;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  button:hover {
    background-color: #218838;
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
</style>
