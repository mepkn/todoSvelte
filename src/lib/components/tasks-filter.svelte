<script>
	import { Button } from './ui/button';

	let { toggleFilter, currentFilter } = $props();
</script>

<div class="mt-4 flex justify-center gap-2">
	<Button
		variant={currentFilter === 'all' ? 'secondary' : 'default'}
		onclick={() => toggleFilter('all')}>All</Button
	>
	<Button
		variant={currentFilter === 'todo' ? 'secondary' : 'default'}
		onclick={() => toggleFilter('todo')}>Todo</Button
	>
	<Button
		variant={currentFilter === 'done' ? 'secondary' : 'default'}
		onclick={() => toggleFilter('done')}>Done</Button
	>
</div>
