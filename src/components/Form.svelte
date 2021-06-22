<script>
  export let name = '';
  export let amount = null;
  export let addExpense;
  export let isEditing;
  export let editExpense;
  export let hideExpenseForm;

  $: isEmpty = !name || !amount;

  function handleSubmit() {
    if (isEditing) {
      editExpense({ name, amount });
    } else {
      addExpense({ amount, name });
    }
    name = '';
    amount = null;
    hideExpenseForm();
  }
</script>

<div>
  <section class="form">
    <form class="expense-form" on:submit|preventDefault={handleSubmit}>
      <div class="form-control">
        <label for="name">name</label>
        <input type="text" id="name" bind:value={name} />
      </div>
      <div class="form-control">
        <label for="amount">amount</label>
        <input type="number" id="amount" bind:value={amount} />
      </div>

      {#if isEmpty}
        <p class="form-empty">please fill out all the fields</p>
      {/if}

      <button
        type="submit"
        class="btn btn-block"
        class:disabled={isEmpty}
        disabled={isEmpty}
      >
        {#if isEditing}edit{:else}add{/if}
      </button>
      <button type="button" class="close-btn" on:click={hideExpenseForm}>
        <i class="fas fa-times" />
      </button>
    </form>
  </section>
</div>

<style>
  div {
    padding: 20px;
  }
</style>
