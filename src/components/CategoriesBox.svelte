<script>
  import List from './List.svelte';
  export let categoriesArray = [
    { id: 1, categoryName: 'To Pay' },
    { id: 2, categoryName: 'Paid' },
    { id: 3, categoryName: 'Debts' },
  ];
</script>

<section>
  {#each categoriesArray as category, index (category.id)}
    <div>
      <List {...category} />
    </div>
  {:else}
    <h2>NO CATEGORIES FOUND</h2>
  {/each}
</section>

<style>
  section {
    display: flex;
    justify-content: space-around;
    width: 90%;
    margin: 0 5%;
    flex-flow: row wrap;
    align-content: space-around;
  }
  h2 {
    text-transform: capitalize;
  }
</style>
