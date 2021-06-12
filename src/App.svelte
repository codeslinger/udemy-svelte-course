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

	// context
	setContext('remove', removeExpense);
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