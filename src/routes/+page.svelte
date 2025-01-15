<script lang="ts">
	import TasksFilter from '@/components/tasks-filter.svelte';
	import TasksForm from '@/components/tasks-form.svelte';
	import TasksList from '@/components/tasks-list.svelte';
	import TasksStat from '@/components/tasks-stat.svelte';
	import type { Filter, Task } from '@/types';

	let tasks = $state<Task[]>([]);
	let currentFilter = $state<Filter>('all');
	let totalDone = $derived(tasks.reduce((acc, task) => acc + (task.done ? 1 : 0), 0));
	let filteredTasks = $derived.by(() => {
		switch (currentFilter) {
			case 'all':
				return tasks;
			case 'todo':
				return tasks.filter((task) => !task.done);
			case 'done':
				return tasks.filter((task) => task.done);
		}
		return tasks;
	});

	let addTasks = (newTask: string) => {
		tasks.push({
			id: crypto.randomUUID(),
			title: newTask,
			done: true
		});
	};

	let toggleDone = (task: Task) => {
		task.done = !task.done;
	};

	let removeTask = (id: string) => {
		let index = tasks.findIndex((task) => task.id === id);
		tasks.splice(index, 1);
	};

	let toggleFilter = (filter: Filter) => {
		currentFilter = filter;
	};
</script>

<div class="container mx-auto px-4 py-4">
	<TasksForm {addTasks} />
	<TasksFilter {currentFilter} {toggleFilter} />
	<TasksStat {totalDone} {tasks} />
	<TasksList tasks={filteredTasks} {toggleDone} {removeTask} />
</div>
