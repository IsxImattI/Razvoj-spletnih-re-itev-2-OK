<script>
  import { Router, Route, Link } from 'svelte-routing';
  import Home from './pages/Home.svelte';
  import About from './pages/About.svelte';
  import Cart from './pages/Cart.svelte';
  import GameDetails from './pages/GameDetails.svelte';
  import Confirmation from "./pages/Confirmation.svelte";
  import TicTacToe from "./pages/TicTacToe.svelte";
let params = {};

</script>

<Router>
  <nav>
    <Link to="/">Domov</Link>
    <Link to="/about">O podjetju</Link>
    <Link to="/cart">Košarica</Link>    
    <Link to="/tictactoe">Križec-Krožec</Link>
  </nav>

  <Route path="/" component={Home} />
  <Route path="/about" component={About} />
  <Route path="/cart" component={Cart} />
  <Route path="/game/:id" let:params>
    <GameDetails params={params} />
  </Route> 
  <Route path="/confirmation" component={Confirmation} /> 
  <Route path="/tictactoe" component={TicTacToe} />
</Router>

<style>
:global(nav) {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  padding: 1rem;
  background-color: #f8f9fa;
  border-bottom: 2px solid #e0e0e0;
  z-index: 1000;
}

:global(nav a) {
  text-decoration: none;
  color: #007bff;
  font-weight: bold;
}

:global(nav a:hover) {
  color: #0056b3;
}

:global(body) {
  margin-top: 80px;
}

@media (max-width: 768px) {
  :global(nav) {
    justify-content: space-around; /* Poravnava na manjših napravah */
    padding: 0.8rem; /* Manjša razdalja za mobilne naprave */
  }

  :global(nav a) {
    font-size: 0.9rem; /* Manjša pisava za mobilne naprave */
    padding: 0.4rem 0.8rem; /* Manjši odmik za boljšo preglednost */
  }
}

@media (max-width: 480px) {
  :global(nav) {
    flex-direction: column; /* Navigacija v stolpec na zelo majhnih zaslonih */
    align-items: center;
    gap: 0.5rem;
  }

  :global(nav a) {
    font-size: 0.8rem;
    padding: 0.3rem 0.6rem;
  }
}

</style>
