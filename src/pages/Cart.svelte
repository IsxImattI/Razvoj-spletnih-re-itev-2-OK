<script>
  import { cart } from "../stores/cart";

  let totalPrice = 0;
  cart.subscribe((items) => {
    totalPrice = items.reduce((sum, item) => sum + item.totalPrice, 0);
  });

  const removeFromCart = (index) => {
    cart.update((items) => {
      items.splice(index, 1);
      return items;
    });
  };

  const clearCart = () => {
    cart.set([]);
  };

  const confirmRental = () => {
    if ($cart.length > 0) {
      window.location.href = "/confirmation";
    } else {
      alert("Košarica je prazna. Dodajte igre, preden potrdite izposojo.");
    }
  };
</script>

<h2>Vaša košarica</h2>
<div class="cart-container">
  {#if $cart.length > 0}
    <div class="cart-items">
      {#each $cart as item, index}
        <div class="cart-item">
          <img src={item.image} alt={item.name} />
          <div class="item-info">
            <h3>{item.name}</h3>
            <p>Kategorija: {item.category}</p>
            <p>Število dni: {item.days}</p>
            <p>Skupna cena: {item.totalPrice.toFixed(2)} €</p>
            <button class="remove-btn" on:click={() => removeFromCart(index)}>Odstrani</button>
          </div>
        </div>
      {/each}
    </div>
    <div class="cart-summary">
      <p class="total-price">Skupna cena vseh iger: {totalPrice.toFixed(2)} €</p>
      <button class="clear-btn" on:click={clearCart}>Počisti košarico</button>
      <button class="confirm-btn" on:click={confirmRental}>Potrdi izposojo</button>
    </div>
  {:else}
    <p class="empty-cart">Košarica je prazna.</p>
  {/if}
</div>

<style>
  h2 {
    text-align: center;
    color: #2c3e50;
    margin-bottom: 1.5rem;
  }

  .cart-container {
    margin: 0 auto;
    max-width: 800px;
    padding: 1rem;
    text-align: center;
  }

  .cart-items {
    margin-bottom: 2rem;
  }

  .cart-item {
    display: flex;
    gap: 1.5rem;
    padding: 1rem;
    border: 1px solid #e0e0e0;
    border-radius: 8px;
    background: #f9f9f9;
    margin-bottom: 1rem;
    align-items: center;
  }

  .cart-item img {
    width: 80px;
    height: auto;
    border-radius: 8px;
  }

  .item-info h3 {
    margin: 0;
    color: #007bff;
  }

  .item-info p {
    margin: 0.3rem 0;
    color: #333;
  }

  .remove-btn {
    background-color: #e74c3c;
    color: white;
    border: none;
    padding: 0.5rem 1rem;
    border-radius: 5px;
    cursor: pointer;
  }

  .remove-btn:hover {
    background-color: #c0392b;
  }

  .cart-summary {
    text-align: center;
  }

  .total-price {
    font-size: 1.2rem;
    font-weight: bold;
    color: #333;
    margin-bottom: 1rem;
  }

  .clear-btn,
  .confirm-btn {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 0.7rem 1.5rem;
    border-radius: 8px;
    cursor: pointer;
    margin: 0.5rem;
  }

  .clear-btn:hover {
    background-color: #0056b3;
  }

  .confirm-btn:hover {
    background-color: #28a745;
  }

  .empty-cart {
    font-size: 1.2rem;
    color: #999;
  }

  @media (max-width: 768px) {
  .cart-item {
    flex-direction: column;
    align-items: flex-start;
  }

  .cart-item img {
    width: 60px;
  }

  .remove-btn {
    padding: 0.4rem 0.8rem;
    font-size: 0.8rem;
  }

  .clear-btn,
  .confirm-btn {
    font-size: 0.9rem;
    padding: 0.5rem 1rem;
  }
}

@media (max-width: 480px) {
  .cart-item img {
    width: 50px;
  }

  .item-info h3 {
    font-size: 1rem;
  }

  .remove-btn {
    font-size: 0.7rem;
  }
}
</style>
