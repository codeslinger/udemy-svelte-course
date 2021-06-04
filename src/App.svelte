<script>
	import { setContext } from 'svelte';

	// components
	import Navbar from './Navbar.svelte';
	import ExpenseList from './ExpenseList.svelte';

	// data
	import expensesData from './expenses';

	// variables
	let expenses = [...expensesData];

	// functions
	function removeExpense(id) {
		expenses = expenses.filter(item => item.id !== id);
	}

	// context
	setContext('remove', removeExpense);
</script>

<Navbar />
<main class="content">
	<ExpenseList {expenses} />
</main>