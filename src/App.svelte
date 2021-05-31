<!-- Logic -->
<script>
	// components
	import Navbar from './Navbar.svelte';
	import ExpenseList from './ExpenseList.svelte';

	// data
	import expensesData from './expenses';

	// variables
	let expenses = [...expensesData];
</script>

<!-- Styling -->
<!-- <style></style> -->

<!-- Markup -->
<Navbar />
<main class="content">
	<ExpenseList {expenses} />
</main>