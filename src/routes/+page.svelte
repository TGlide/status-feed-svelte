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

	let modalEl: HTMLDialogElement | null;
</script>

<div class="container">
	<button class="button" on:click={() => modalEl?.showModal()}>Add status</button>
	<div class="u-flex u-flex-vertical u-gap-16 u-margin-block-start-32">
		{#each mockStatus as status}
			<div class="box u-flex u-cross-center u-gap-24">
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

<dialog class="modal" bind:this={modalEl}>
	<form class="modal-form" method="dialog">
		<header class="modal-header">
			<div class="avatar is-color-orange is-medium">
				<span class="icon-exclamation" aria-hidden="true" />
			</div>
			<h4 class="modal-title heading-level-5">Modal title</h4>
			<button class="x-button" aria-label="Close modal">
				<span class="icon-x" aria-hidden="true" />
			</button>
		</header>
		<div class="modal-content u-small">Modal label text.</div>
		<div class="modal-footer">
			<div class="u-flex u-main-end u-gap-16">
				<button class="button is-text"><span class="text">Button</span></button><button
					class="button is-secondary"><span class="text">Button</span></button
				>
			</div>
		</div>
	</form>
</dialog>

<style>
	.icon-wrapper {
		display: grid;
		place-items: center;

		--size: 3rem;
		width: var(--size);
		height: var(--size);

		background-color: hsla(var(--color-neutral-400));
		border-radius: var(--border-radius-circular);
		color: hsl(var(--color-primary-100));
	}
</style>
