<script lang="ts">
	export let name: string;
	export let label: string;

	const icons = [
		'chat',
		'code',
		'cake',
		'heart',
		'home',
		'info',
		'mail',
		'phone',
		'search',
		'star',
		'user',
		'x'
	];

	let value: string = icons[0];
</script>

<label for={name} class="label">{label}</label>
<input type="hidden" {name} {value} />

<ul class="secondary-tabs u-gap-4">
	{#each icons as icon}
		<li class="secondary-tabs-item">
			<button
				class="secondary-tabs-button u-padding-16"
				disabled={icon === value}
				on:click={() => (value = icon)}
				type="button"
			>
				<span class={`icon-${icon}`} />
			</button>
		</li>
	{/each}
</ul>
