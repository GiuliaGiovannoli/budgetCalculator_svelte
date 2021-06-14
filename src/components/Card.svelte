<script>
  export let expenses;
</script>

<section>
  <h3>Here your monthly expenses</h3>
  <ul>
    {#each expenses as item}
      <li>{item.name} € {item.amount}</li>
    {/each}
  </ul>
</section>
