<script>
	export let href = '/';
	export let CSSClass = '';
</script>

<div class={CSSClass}>
	<a {href}><slot /></a>
</div>

<style>
	div {
		box-sizing: border-box;
		padding: var(--border-width);
		background: var(--border-color);
		border-radius: var(--border-radius);
		display: flex;
		justify-content: center;
		align-items: center;
	}
	a {
		box-sizing: border-box;
		text-decoration: none;
		border-radius: var(--border-radius);
		background-color: var(--background-color);
		width: calc(var(--width) - var(--border-width) * 2);
		height: calc(var(--height) - var(--border-width) * 2);
		padding: 0.5em;
		text-align: center;
		color: var(--color);
		font: var(--font);
	}
	a:visited {
		color: var(--color);
	}
</style>
