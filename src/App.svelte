<script>
	import { setContext } from 'svelte';

	// components
	import Navbar from './Navbar.svelte';
	import ExpenseList from './ExpenseList.svelte';
	import ExpenseForm from './ExpenseForm.svelte';
	import Totals from './Totals.svelte';

	// data
	import expensesData from './expenses';

	// variables
	let expenses = [...expensesData];

	// set editing variables
	let setName = '';
	let setAmount = null;
	let setID = null;

	// reactive
	$: total = expenses.reduce((accum, elem) => accum + elem.amount, 0);

	// functions
	function addExpense({name, amount}) {
		const expense = {
			id: Math.random() * Date.now(),
			name,
			amount
		};
		expenses = [expense, ...expenses];
	}
	function removeExpense(id) {
		expenses = expenses.filter(item => item.id !== id);
	}
	function clearExpenses() {
		expenses = [];
	}
	function setModifiedExpense(id) {
		const expense = expenses.find(item => item.id === id);
		console.log(expense);
		setID = expense.id;
		setName = expense.name;
		setAmount = expense.amount;
		console.log({setID, setName, setAmount});
	}

	// context
	setContext('remove', removeExpense);
	setContext('modify', setModifiedExpense);
</script>

<Navbar />
<main class="content">
	<ExpenseForm {addExpense} />
	<Totals title="total expenses" {total} />
	<ExpenseList {expenses} />
	<button type="button" class="btn btn-primary btn-block" on:click={clearExpenses}>
		clear expenses
	</button>
</main>