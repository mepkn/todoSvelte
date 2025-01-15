<script lang="ts">
	import * as Card from '$lib/components/ui/card';
	import type { Task } from '@/types';
	import { Trash2 } from 'lucide-svelte';
	import { fade } from 'svelte/transition';
	import { Button } from './ui/button';
	import { Checkbox } from './ui/checkbox';
	import { Label } from './ui/label';

	let {
		tasks,
		toggleDone,
		removeTask
	}: { tasks: Task[]; toggleDone: (task: Task) => void; removeTask: (id: string) => void } =
		$props();
</script>

{#if tasks.length > 0}
	<section class="mt-4 flex justify-center">
		<Card.Root class="w-full max-w-sm">
			<Card.Content>
				<div class="space-y-2">
					{#each tasks as task}
						<div class="flex items-center justify-between gap-2" transition:fade>
							<div class="flex items-start gap-2">
								<Checkbox
									id={task.id}
									checked={task.done}
									onCheckedChange={() => toggleDone(task)}
								/>
								<Label for={task.id}>{task.title}</Label>
							</div>
							<Button
								variant="outline"
								size="icon"
								onclick={() => removeTask(task.id)}
								class="flex-shrink-0"
							>
								<Trash2 class="h-4 w-4" />
							</Button>
						</div>
					{/each}
				</div>
			</Card.Content>
		</Card.Root>
	</section>
{/if}
