<script>
  export let showForm;
</script>

<nav class="nav">
  <div class="nav-center">
    <h1 class="nav-title">THE BUDGET CALCULATOR</h1>
    <button type="button" class="nav-btn" on:click={showForm}>
      <i class="far fa-plus-square" />
      ADD NEW CATEGORY
    </button>
  </div>
</nav>

<style>
  button {
    color: #fff;
  }
</style>
