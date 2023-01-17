<script lang="ts">
	type Status = {
		icon: string;
		name: string;
		text: string;
	};

	const mockStatus: Status[] = [
		{
			name: 'Thomas',
			icon: 'chat',
			text: 'In a meeting!'
		},
		{
			name: 'Torsten',
			icon: 'code',
			text: 'Coding frenetically'
		},
		{
			name: 'Wess',
			icon: 'cake',
			text: 'FEED'
		}
	];
</script>

<div class="container">
	<button class="">Add status</button>
	{#each mockStatus as status}
		<div class="">
			<span class="">
				<span class={`${status.icon}`} />
			</span>
			<span>{status.name}</span>
			<span>{status.text}</span>
		</div>
	{/each}
</div>
