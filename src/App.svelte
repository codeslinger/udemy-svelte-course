<script>
	import { setContext } from 'svelte';

	// components
	import Navbar from './Navbar.svelte';
	import ExpenseList from './ExpenseList.svelte';
	import Totals from './Totals.svelte';

	// data
	import expensesData from './expenses';

	// variables
	let expenses = [...expensesData];

	// reactive
	$: total = expenses.reduce((accum, elem) => accum + elem.amount, 0);

	// functions
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
	<Totals title="total expenses" {total} />
	<ExpenseList {expenses} />
	<button type="button" class="btn btn-primary btn-block" on:click={clearExpenses}>
		clear expenses
	</button>
</main>