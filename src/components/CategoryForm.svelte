<script>
  export let categoryName = '';
  export let addCategory;
  export let hideForm;

  $: isEmpty = !categoryName;

  function handleSubmit() {
    addCategory({ categoryName });
    categoryName = '';
    hideForm();
  }
</script>

<div>
  <section class="form">
    <form class="expense-form" on:submit|preventDefault={handleSubmit}>
      <div class="form-control">
        <label for="categoryName">category name</label>
        <input type="text" id="categoryName" bind:value={categoryName} />
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
        SUBMIT
      </button>
      <button type="button" class="close-btn" on:click={hideForm}>
        <i class="fas fa-times" />
      </button>
    </form>
  </section>
</div>

<style>
  div {
    padding: 5px;
    display: flex;
    justify-content: center;
  }
  section {
    width: 40%;
  }
</style>
