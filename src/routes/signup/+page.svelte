<script>
	import { base } from '$app/paths';
	import { Logo, CTA } from '$lib/index.js';

	let selected = 'personal';
	let vw;
	let loginPopup;
</script>

<svelte:window bind:innerWidth={vw} />
<svelte:head><link rel="stylesheet" href="{base}/styles.css" /></svelte:head>
<svelte:document
	on:click={() => {
		loginPopup.style.display = 'none';
	}}
/>
<header>
	<Logo
		width={vw >= 1200 ? 120 : vw >= 500 ? 80 : 60}
		height={vw >= 1200 ? 60 : vw >= 500 ? 80 : 30}
	></Logo>
	<ul>
		<li>
			<!-- svelte-ignore a11y-click-events-have-key-events -->
			<!-- svelte-ignore a11y-no-static-element-interactions -->
			<div
				class="login-div"
				on:click={(e) => {
					// debugger;
					e.preventDefault();
					e.stopPropagation();
					loginPopup.style.display = 'flex';
				}}
			>
				<a class="login" href="/signup">Log In</a>
				<div class="login-popup" bind:this={loginPopup}>
					<input placeholder="Email" /><input placeholder="Password" /><button>Log In</button>
				</div>
			</div>
		</li>
	</ul>
</header>
<main>
	<div class="account_selection">
		<h1 class="account_heading">Choose an account plan</h1>
		<div class="account_select">
			<div class="account_plan">
				<label><input type="radio" bind:group={selected} value="personal" checked /> Personal</label
				>
				<p class="account_description">
					Pay on any device all around the world without sharing your personal info with third
					parties.
				</p>
			</div>
			<div class="account_plan">
				<label><input type="radio" bind:group={selected} value="business" /> Business</label>
				<p class="account_description">
					Recieve payments from your customers from various platforms with detailed analytics
					included.
				</p>
			</div>
		</div>
	</div>
	<div class="account_data">
		<div class="form">
			<div class="input">
				<span>First Name</span>
				<div class="input-border"><input /></div>
			</div>
			<div class="input">
				<span>Last Name</span>
				<div class="input-border"><input /></div>
			</div>
			<div class="input">
				<span>Email</span>
				<div class="input-border"><input /></div>
			</div>
			<div class="input">
				<span>Password</span>
				<div class="input-border"><input /></div>
			</div>
			{#if selected === 'business'}<div class="input">
					<span>Business Name</span>
					<div class="input-border"><input /></div>
				</div>{/if}
			{#if selected === 'personal'}<div class="input">
					<span>Billing Address</span>
					<div class="input-border"><input /></div>
				</div>{/if}
		</div>
		<CTA
			CSSClass="create-cta"
			href="/signup"
			--border-color="var(--gradient-blue"
			--border-radius="999px"
			--border-width="2px"
			--background-color="var(--neutral-7)"
			--width={vw >= 1200 ? '480px' : vw >= 500 ? '360px' : '240px'}
			--height={vw >= 1200 ? '96px' : vw >= 500 ? '64px' : '48px'}
			--color="var(--neutral-1)"
			--font="var(--bigger)">Create Account</CTA
		>
	</div>
</main>
<footer>
	<hr class="footer_hr" />
	<ul class="footer_links">
		<li class="footer_link-item"><a class="footer_link" href="/">About</a></li>
		<li class="footer_link-item"><a class="footer_link" href="/">Contact</a></li>
		<li class="footer_link-item"><a class="footer_link" href="/">Privacy</a></li>
	</ul>
	<span class="copy"
		>Created by <a class="copy_link" href="https://github.com/nmilutin">NMilutin</a></span
	>
</footer>

<style>
	:global(body) {
		margin: 0;
		background-color: var(--neutral-7);
	}
	header,
	ul {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
	header {
		justify-content: space-between;
		padding: 25px 12px;
	}
	ul {
		height: 30px;
		list-style: none;
		padding: 0;
		margin: 0;
		gap: 8px;
	}
	a {
		display: block;
		text-decoration: none;
		font: var(--medium);
		color: var(--neutral-1);
	}
	.login-div {
		box-sizing: border-box;
		background: var(--gradient-blue);
		padding: 2px;
		border-radius: 50px;
		width: 80px;
		text-align: center;
		position: relative;
	}
	.login {
		box-sizing: border-box;
		background-color: var(--neutral-7);
		border-radius: 50px;
		padding: 4px 8px;
	}
	.login-popup {
		display: none;
		position: absolute;
		bottom: -150px;
		right: 8px;
		box-sizing: border-box;
		border: 2px solid var(--neutral-5);
		border-radius: 16px;
		background-color: var(--neutral-7);
		padding: 16px;
		flex-direction: column;
		box-shadow: 0 4px 4px 4px rgba(0, 0, 0, 0.1);
	}
	.login-popup input {
		border: 2px solid var(--neutral-5);
		border-radius: 8px;
		padding: 4px;
		font: var(--medium);
		background-color: var(--neutral-7);
		margin-bottom: 3%;
		outline: none;
	}
	.login-popup button {
		border: 2px solid var(--neutral-5);
		border-radius: 999px;
		margin: 0 25%;
		padding: 4px;
		font: var(--medium);
		color: var(--neutral-7);
		background: var(--gradient-blue);
	}
	.account_selection {
		background: var(--gradient-blue);
		height: 240px;
		color: var(--neutral-7);
		display: flex;
		flex-direction: column;
		padding: 20px;
		gap: 32px;
	}
	.account_heading {
		font: var(--medium);
		align-self: center;
	}
	.account_select {
		display: flex;
		flex-direction: column;
		flex: 1;
		gap: 12px;
	}
	.account_plan {
		padding: 8px 12px;
	}
	.account_plan input {
		appearance: none;
		width: 12px;
		height: 12px;
		border: 2px solid var(--neutral-7);
		background-color: var(--neutral-6);
		border-radius: 50%;
		box-sizing: border-box;
	}
	.account_plan input:checked {
		background: var(--gradient-blue);
	}
	.account_plan label {
		font: var(--big);
	}
	.account_plan p {
		font: var(--body);
		margin: 0;
		margin-left: 24px;
	}
	.account_data {
		height: 400px;
		padding: 40px 20px;
		display: flex;
		flex-direction: column;
		align-items: center;
		padding: 32px;
	}
	.form {
		width: 100%;
	}
	.input span {
		font: var(--medium);
		margin: 12px 0 4px 4px;
		display: block;
	}
	.input-border {
		background: var(--gradient-blue);
		padding: 2px;
		border-radius: 8px;
		box-sizing: border-box;
	}
	.input-border input {
		font: var(--medium);
		color: var(--neutral-1);
		width: 100%;
		padding: 8px;
		box-sizing: border-box;
		border-radius: 6px;
		border: none;
		outline: none;
		display: block;
		height: 32px;
		box-shadow: inset 2px 2px 2px 1px rgba(0, 0, 0, 0.2);
		background-color: var(--neutral-7);
	}
	:global(.create-cta) {
		margin-top: 24px;
		width: fit-content;
		box-shadow: 0 4px 4px 4px rgba(0, 0, 0, 0.2);
	}
	footer {
		padding: 12px 32px;
		display: flex;
		flex-direction: column;
	}
	footer * {
		color: var(--neutral-4);
	}
	.footer_hr {
		color: var(--neutral-4);
		border: 1px solid var(--neutral-5);
		margin: 8px -12px;
	}
	.footer_links {
		display: flex;
		justify-content: space-between;
		text-align: center;
	}
	.footer_link-item {
		flex: 1;
	}
	.copy {
		font: var(--body);
		width: 100%;
		align-self: center;
		text-align: center;
	}
	.copy_link,
	.copy_link:visited {
		font: var(--body);
		color: var(--neutral-3);
		display: inline;
		text-decoration: underline;
	}
	@media screen and (min-width: 500px) {
		header {
			padding: 35px 18px;
		}
		ul {
			height: 45px;
			gap: 12px;
		}
		.login-div {
			padding: 3px;
			border-radius: 75px;
			width: 120px;
		}
		.login {
			border-radius: 75px;
			padding: 6px 12px;
		}
		.login-popup {
			bottom: -176px;
		}
		.account_selection {
			height: 360px;
			padding: 30px;
			gap: 48px;
		}
		.account_select {
			gap: 16px;
		}
		.account_plan {
			padding: 12px 18px;
		}
		.account_plan input {
			width: 18px;
			height: 18px;
			border: 3px solid var(--neutral-7);
		}
		.account_plan p {
			margin-left: 36px;
		}
		.account_data {
			height: 600px;
			padding: 60px 30px;
			padding: 48px;
		}
		.form {
			width: 80%;
		}
		.input span {
			margin: 18px 0 6px 6px;
		}
		.input-border {
			padding: 3px;
			border-radius: 12px;
		}
		.input-border input {
			width: 100%;
			padding: 12px;
			border-radius: 8px;
			height: 48px;
			box-shadow: inset 3px 3px 3px 2px rgba(0, 0, 0, 0.2);
		}
		:global(.create-cta) {
			margin-top: 36px;
			box-shadow: 0 6px 6px 6px rgba(0, 0, 0, 0.2);
		}
		footer {
			padding: 18px 48px;
		}
		.footer_hr {
			border: 2px solid var(--neutral-5);
			margin: 12px -18px;
		}
	}
	@media screen and (min-width: 1200px) {
		header {
			padding: 50px 24px;
		}
		ul {
			height: 60px;
			gap: 16px;
		}
		.login-div {
			padding: 4px;
			border-radius: 100px;
			width: 160px;
		}
		.login {
			border-radius: 100px;
			padding: 8px 16px;
		}
		.login-popup {
			bottom: -224px;
		}
		.account_selection {
			height: 480px;
			padding: 40px;
			gap: 64px;
		}
		.account_select {
			flex: 1;
			gap: 24px;
		}
		.account_plan {
			padding: 16px 24px;
		}
		.account_plan input {
			width: 24px;
			height: 24px;
			border: 4px solid var(--neutral-7);
		}
		.account_plan p {
			margin-left: 48px;
		}
		.account_data {
			height: 800px;
			padding: 80px 40px;
			padding: 64px;
		}
		.form {
			width: 60%;
		}
		.input span {
			margin: 24px 0 8px 8px;
		}
		.input-border {
			padding: 4px;
			border-radius: 16px;
		}
		.input-border input {
			width: 100%;
			padding: 16px;
			border-radius: 12px;
			height: 64px;
			box-shadow: inset 4px 4px 4px 2px rgba(0, 0, 0, 0.2);
		}
		:global(.create-cta) {
			margin-top: 48px;
			box-shadow: 0 8px 8px 8px rgba(0, 0, 0, 0.2);
		}
		footer {
			padding: 24px 64px;
		}
		.footer_hr {
			border: 2px solid var(--neutral-5);
			margin: 16px -24px;
		}
	}
</style>
