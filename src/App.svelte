<script>
  import { setContext } from 'svelte';

  import Navbar from './components/NavBar.svelte';
  import CategoriesBox from './components/CategoriesBox.svelte';
  import CategoryForm from './components/CategoryForm.svelte';

  let categoriesArray = [
    { id: Math.random() * Date.now(), categoryName: 'To Pay' },
    { id: Math.random() * Date.now(), categoryName: 'Paid' },
    { id: Math.random() * Date.now(), categoryName: 'Debts' },
  ];

  let setCategoryName = '';

  let isFormOpen = false;

  function showForm() {
    isFormOpen = true;
  }

  function hideForm() {
    isFormOpen = false;
    setName = '';
    setAmount = null;
    setId = null;
  }

  function clearExpenses() {
    categoriesArray = [];
  }

  function addCategory({ categoryName }) {
    let category = { id: Math.random() * Date.now(), categoryName };
    categoriesArray = [category, ...categoriesArray];
  }
</script>

<Navbar {showForm} />

<main class="content">
  {#if isFormOpen}
    <CategoryForm {addCategory} categoryName={setCategoryName} {hideForm} />
  {/if}

  <CategoriesBox {categoriesArray} />

  <button
    type="button"
    class="btn btn-primary btn-block"
    on:click={clearExpenses}
  >
    Delete all categories
  </button>
</main>
