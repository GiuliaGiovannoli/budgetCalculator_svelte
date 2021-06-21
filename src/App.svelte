<script>
  import { setContext } from 'svelte';

  import Navbar from './components/NavBar.svelte';
  import List from './components/List.svelte';
  import Form from './components/Form.svelte';

  let expensesArray = [];

  let setName = '';
  let setAmount = null;
  let setId = null;

  let isFormOpen = false;

  $: isEditing = setId ? true : false;

  function showForm() {
    isFormOpen = true;
  }

  function hideForm() {
    isFormOpen = false;
    setName = '';
    setAmount = null;
    setId = null;
  }

  function deleteExpense(id) {
    expensesArray = expensesArray.filter((item) => item.id !== id);
  }

  function clearExpenses() {
    expensesArray = [];
  }

  function addExpense({ name, amount }) {
    let expense = { id: Math.random() * Date.now(), name, amount };
    expensesArray = [expense, ...expensesArray];
  }
  function setEditedExpense(id) {
    let expense = expensesArray.find((item) => item.id === id);
    setId = expense.id;
    setName = expense.name;
    setAmount = expense.amount;
    showForm();
  }

  function editExpense({ name, amount }) {
    expensesArray = expensesArray.map((item) => {
      return item.id === setId ? { ...item, name, amount } : { ...item };
    });
    setId = null;
    setAmount = null;
    setName = '';
  }

  setContext('delete', deleteExpense);

  setContext('edit', setEditedExpense);
</script>

<Navbar {showForm} />

<main class="content">
  {#if isFormOpen}
    <Form
      {addExpense}
      name={setName}
      amount={setAmount}
      {isEditing}
      {editExpense}
      {hideForm}
    />
  {/if}

  <List {expensesArray} />

  <button
    type="button"
    class="btn btn-primary btn-block"
    on:click={clearExpenses}
  >
    Delete all
  </button>
</main>
