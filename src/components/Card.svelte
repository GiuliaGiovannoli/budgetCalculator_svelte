<script>
  import { getContext } from 'svelte';

  export let id;
  export let name = '';
  export let amount = 0;

  const deleteExpense = getContext('delete');

  const setEditedExpense = getContext('edit');
</script>

<article class="single-expense">
  <div class="expense-info">
    <h2>
      {name}
    </h2>
    <h4>amount : €{amount}</h4>
  </div>
  <div class="expense-buttons">
    <button class="expense-btn edit-btn" on:click={() => setEditedExpense(id)}>
      <i class="fas fa-pen" />
      EDIT
    </button>
    <button class="expense-btn delete-btn" on:click={() => deleteExpense(id)}>
      <i class="fas fa-trash" />
      DELETE
    </button>
  </div>
</article>
