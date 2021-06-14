<script>
  import NavBar from './components/NavBar.svelte';
  export let name;
  import Card from './components/Card.svelte';
  import expensesData from '../public/expenses';
  let expenses = [...expensesData];
</script>

<main>
  <NavBar />
  <h1>Hello {name}!</h1>
  <Card {expenses} />
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
