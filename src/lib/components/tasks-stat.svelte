<script>
	let { totalDone, tasks } = $props();
</script>

<div class="mt-4 flex justify-center">
	{#if tasks.length}
		<p>{totalDone} / {tasks.length} tasks completed</p>
	{:else}
		<p>No tasks yet, Add some task</p>
	{/if}
</div>
