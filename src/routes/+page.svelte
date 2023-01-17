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
	<button class="button is-secondary">Add status</button>
	<div class="u-flex u-flex-vertical u-gap-16 u-margin-block-start-32">
		{#each mockStatus as status}
			<div class="box u-flex u-cross-center u-gap-12">
				<div class="icon-wrapper">
					<span class={`icon-${status.icon}`} />
				</div>
				<div class="u-flex u-flex-vertical">
					<h6 class="heading-level-6">{status.name}</h6>
					<p>{status.text}</p>
				</div>
			</div>
		{/each}
	</div>
</div>

<style>
	.icon-wrapper {
		display: grid;
		place-items: center;

		--size: 3rem;
		width: var(--size);
		height: var(--size);

		background-color: hsl(var(--color-neutral-30));
		border-radius: var(--border-radius-circular);
	}
</style>
