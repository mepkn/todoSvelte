<script lang="ts">
	import Button from './ui/button/button.svelte';
	import { Input } from './ui/input';

	let { addTasks }: { addTasks: (newTask: string) => void } = $props();
	let newTask = $state('');

	let formSubmitted = (e: SubmitEvent) => {
		e.preventDefault();
		addTasks(newTask);
		newTask = '';
	};
</script>

<form onsubmit={formSubmitted}>
	<div class="flex justify-center gap-4">
		<Input
			type="text"
			id="newTask"
			placeholder="New Task"
			bind:value={newTask}
			required
			class="max-w-sm ring-2 ring-black"
		/>
		<Button type="submit">Add</Button>
	</div>
</form>
