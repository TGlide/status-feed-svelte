<script lang="ts">
	import IconPicker from '$components/IconPicker.svelte';
	import { fly, slide } from 'svelte/transition';
	import { flip } from 'svelte/animate';

	type Status = {
		icon: string;
		name: string;
		text: string;
	};

	const isStatus = (status: unknown): status is Status => {
		return (
			typeof status === 'object' &&
			status !== null &&
			'icon' in status &&
			'name' in status &&
			'text' in status
		);
	};

	let mockStatus: Status[] = [
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

	const handleSubmit = (e: Event) => {
		e.preventDefault();
		const form = e.target as HTMLFormElement;
		const formData = new FormData(form);
		const data = Object.fromEntries(formData.entries());

		if (!isStatus(data)) {
			console.error('Invalid status:', data);
			return;
		}

		mockStatus = [data, ...mockStatus];
		modalEl?.close();
	};
</script>

<div class="container">
	<button class="button" on:click={() => modalEl?.showModal()}>Add status</button>
	<div class="u-flex u-flex-vertical u-gap-16 u-margin-block-start-32">
		{#each mockStatus as status, i (`${status.name}-${status.text}`)}
			<div
				class="box u-flex u-cross-center u-gap-24"
				in:fly={{ x: -16, y: 0, delay: 350 }}
				animate:flip={{ duration: 500 }}
			>
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
	<form class="modal-form" method="dialog" on:submit={handleSubmit}>
		<header class="modal-header">
			<h4 class="modal-title heading-level-5">Add status</h4>
			<button
				class="x-button"
				aria-label="Close modal"
				on:click|preventDefault={() => modalEl?.close()}
			>
				<span class="icon-x" aria-hidden="true" />
			</button>
		</header>
		<div class="modal-content u-small">
			<ul class="form-list">
				<li class="form-item">
					<label class="label is-required" for="name">Name</label>
					<input type="text" class="input-text" name="name" placeholder="Jane Doe" required />
				</li>
				<li class="form-item">
					<label class="label is-required" for="name">Text</label>
					<input
						type="text"
						class="input-text"
						name="text"
						placeholder="👋 Good morning!"
						required
					/>
				</li>
				<li class="form-item">
					<IconPicker label="Icon" name="icon" />
				</li>
			</ul>
		</div>
		<div class="modal-footer">
			<div class="u-flex u-main-end u-gap-16">
				<button class="button is-text" on:click|preventDefault={() => modalEl?.close()}>
					<span class="text">Cancel</span>
				</button>
				<button class="button is-secondary">
					<span class="icon-plus" aria-hidden="true" />
					<span class="text">Add</span>
				</button>
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
