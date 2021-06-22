<script>
  import { setContext } from 'svelte';

  import Card from './Card.svelte';
  import Form from './Form.svelte';

  export let categoryName = '';
  export let expensesArray = [];

  $: isEditing = setId ? true : false;

  let isExpenseFormOpen = false;

  function showExpenseForm() {
    isExpenseFormOpen = true;
  }

  let setName = '';
  let setAmount = null;
  let setId = null;

  function hideExpenseForm() {
    isExpenseFormOpen = false;
    setName = '';
    setAmount = null;
    setId = null;
  }

  function deleteExpense(id) {
    expensesArray = expensesArray.filter((item) => item.id !== id);
  }

  function addExpense({ name, amount }) {
    let expense = {
      id: Math.random() * Date.now(),
      name,
      amount,
      paid: false,
      debts: false,
    };
    expensesArray = [expense, ...expensesArray];
  }

  //function addPaidExpense({ name, amount, id }) {}

  //function addDebtsExpense({ name, amount, id }) {}

  function setEditedExpense(id) {
    let expense = expensesArray.find((item) => item.id === id);
    setId = expense.id;
    setName = expense.name;
    setAmount = expense.amount;
    showExpenseForm();
  }

  function editExpense({ name, amount }) {
    expensesArray = expensesArray.map((item) => {
      return item.id === setId
        ? { ...item, name, amount, paid: false, debts: false }
        : { ...item };
    });
    setId = null;
    setAmount = null;
    setName = '';
  }

  setContext('delete', deleteExpense);
  setContext('edit', setEditedExpense);
</script>

<div>
  <h2>{categoryName.toUpperCase()}</h2>
  {#if (categoryName === 'To Pay') & !isExpenseFormOpen}
    <button type="button" class="btn btn-primary" on:click={showExpenseForm}>
      ADD NEW EXPENSE
    </button>
  {/if}

  {#if isExpenseFormOpen}
    <Form
      {addExpense}
      name={setName}
      amount={setAmount}
      {isEditing}
      {editExpense}
      {hideExpenseForm}
    />
  {/if}
  <br />
  <br />

  {#each expensesArray as expense, index (expense.id)}
    <div>
      <Card {...expense} />
    </div>
  {:else}
    <h6>No espenses found</h6>
  {/each}
</div>

<style>
  div {
    margin: 2%;
    padding: 20px;
    background-color: lightgray;
  }
  h2 {
    text-transform: capitalize;
  }
</style>
