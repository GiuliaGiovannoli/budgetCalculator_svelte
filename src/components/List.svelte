<script>
  import Card from './Card.svelte';
  export let expensesArray = [];
</script>

<section>
  <ul>
    {#each expensesArray as expense, index (expense.id)}
      <div>
        <Card {...expense} />
      </div>
    {:else}
      <h2>no expenses added to the list</h2>
    {/each}
  </ul>
</section>

<style>
  h2 {
    text-transform: capitalize;
  }
</style>
