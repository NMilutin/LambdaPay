<script>
	import { base } from '$app/paths';
	import { Logo, Hero, CTA } from '$lib/index.js';

	let tabs = [
		{
			data: {
				h: 'Global money transfer from your pocket',
				b: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in.'
			},
			active: true
		},
		{
			data: {
				h: 'Low transfer fees',
				b: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in.'
			},
			active: false
		},
		{
			data: {
				h: 'Delete your account any time',
				b: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in.'
			},
			active: false
		}
	];
	const testimonials = [
		{
			photo: `${base}/Testimonials/1.png`,
			name: 'Jeffery Robertson',
			text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.'
		},
		{
			photo: `${base}/Testimonials/2.png`,
			name: 'Brennan Pierce',
			text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.'
		},
		{
			photo: `${base}/Testimonials/3.png`,
			name: 'Walter White',
			text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.'
		}
	];
	let sliderIndex = 0;
	let testimonialsEl;
	$: testimonialsElArr = testimonialsEl?.querySelectorAll('.testimonial');
	const changeActiveTab = function (e) {
		const tgt = e.target.closest('.tab');
		if (!tgt) return;
		const i = +tgt.dataset.i;
		tabs.forEach((tab, ti) => {
			if (ti + 1 === i) tab.active = true;
			else tab.active = false;
		});
		tabs = tabs;
	};
	const slide = function (e) {
		const tgt = e.target.closest('.btn');
		if (!tgt) return;
		if (tgt.classList.contains('btn-left') && sliderIndex > 0) sliderIndex--;
		if (tgt.classList.contains('btn-right') && sliderIndex < testimonials.length - 1) sliderIndex++;
		testimonialsElArr.forEach((t, i) => {
			t.style.transform = `translateX(${-sliderIndex * 100}%)`;
		});
	};
	let testimonialsPage;
	let downloadPage;
	let vw;
</script>

<svelte:window bind:innerWidth={vw} />
<svelte:head><link rel="stylesheet" href="{base}/styles.css" /></svelte:head>
<header>
	<Logo
		width={vw >= 1200 ? 120 : vw >= 500 ? 80 : 60}
		height={vw >= 1200 ? 60 : vw >= 500 ? 80 : 30}
	></Logo>
	<ul>
		<li>
			<a
				on:click={(e) => {
					e.preventDefault();
					testimonialsPage.scrollIntoView({ behavior: 'smooth' });
				}}
				href="/">Testimonials</a
			>
		</li>
		<li>
			<a
				on:click={(e) => {
					e.preventDefault();
					downloadPage.scrollIntoView({ behavior: 'smooth' });
				}}
				href="/">Download</a
			>
		</li>
		<li><div class="signup-div"><a class="signup" href="/signup">Sign Up</a></div></li>
	</ul>
</header>
<main>
	<div class="hero">
		<Hero
			CSSclass="hero-svg"
			width={vw >= 1200 ? 510 : vw >= 500 ? 360 : 220}
			height={vw >= 1200 ? 350 : vw >= 500 ? 240 : 172}
		></Hero><span class="hero-text">Smooth payments<br />No hidden fees</span>
		<CTA
			CSSClass="hero-cta"
			href="/signup"
			--border-color="var(--gradient-blue"
			--border-radius="999px"
			--border-width="2px"
			--background-color="var(--neutral-7)"
			--width={vw >= 1200 ? '480px' : vw >= 500 ? '360px' : '240px'}
			--height={vw >= 1200 ? '96px' : vw >= 500 ? '64px' : '48px'}
			--color="var(--neutral-1)"
			--font="var(--bigger)">Start Now</CTA
		>
	</div>
	<div class="features">
		<h1 class="features_heading">Pay and recieve, whenever you want, wherever you want</h1>
		<div class="tabs_container">
			<!-- svelte-ignore a11y-click-events-have-key-events -->
			<!-- svelte-ignore a11y-no-static-element-interactions -->
			<div class="tabs" on:click={changeActiveTab}>
				{#each tabs as tab, i}<div
						data-i={i + 1}
						class="tab{tab.active ? '_active' : ''} tab-{tabs.findIndex((tab) => tab.active) + 1}"
					>
						<img
							src="{base}/Icon{i + 1}{tab.active ? 'Active' : 'Inactive'}.svg"
							alt="Icon{i + 1}"
						/>
					</div>{/each}
			</div>
			{#each tabs as tab, i}<div
					data-i={i + 1}
					class="tab_content{tab.active ? '_active' : ''} tab_content-{i + 1}"
				>
					<div class="tab_content-text">
						<h2 class="tab_content-heading">{tab.data.h}</h2>
						<p class="tab_content-body">{tab.data.b}</p>
					</div>
				</div>
			{/each}
		</div>
	</div>
	<div class="testimonials" bind:this={testimonialsPage}>
		<h1 class="testimonials_heading">Thousands have already made the decision</h1>
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<!-- svelte-ignore a11y-no-static-element-interactions -->
		<div class="testimonials_container" on:click={slide}>
			<button class="btn btn-left"><img src="{base}/Left.png" alt="🢐" /></button>
			<div class="testimonials_slides" bind:this={testimonialsEl}>
				{#each testimonials as t, i}<div class="testimonial" data-i={i}>
						<img class="testimonial_photo" src={t.photo} alt="Person" />
						<h3 class="testimonial_name">{t.name}</h3>
						<p class="testimonial_text">{t.text}</p>
					</div>{/each}
			</div>
			<button class="btn btn-right"><img src="{base}/Right.png" alt="🢒" /></button>
		</div>
	</div>
	<div class="download" bind:this={downloadPage}>
		<h1 class="download_heading">Already have an account?<br />Download the app</h1>
		<div class="download_links">
			<a href="/"><img src="{base}/PlayStore.png" alt="Play Store" /></a>
			<a href="/"><img src="{base}/AppStore.png" alt="Play Store" /></a>
		</div>
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

<!-- 
	TODO responsive sign up, additional pages & popups   -->

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
	.signup-div {
		box-sizing: border-box;
		background: var(--gradient-blue);
		padding: 2px;
		border-radius: 50px;
	}
	.signup {
		box-sizing: border-box;
		background-color: var(--blue-6);
		border-radius: 50px;
		padding: 4px 8px;
	}
	.hero {
		background: var(--gradient-blue);
		display: flex;
		justify-content: center;
		height: 240px;
		position: relative;
	}
	:global(.hero-svg) {
		align-self: center;
		margin-right: -10%;
		margin-left: 5%;
	}
	.hero-text {
		font: var(--bigger-sb);
		color: var(--neutral-7);
		text-align: right;
		align-self: flex-start;
		margin-top: 5%;
		margin-right: 10%;
	}
	:global(.hero-cta) {
		position: absolute;
		bottom: -24px;
		left: 50%;
		transform: translateX(-50%);
		box-shadow: 0 4px 4px 4px rgba(0, 0, 0, 0.2);
	}
	.features {
		height: 400px;
		padding: 40px 20px;
		display: flex;
		flex-direction: column;
		box-sizing: border-box;
	}
	.features_heading {
		font: var(--bigger);
		text-align: center;
	}
	.tabs_container {
		display: flex;
		flex-direction: column;
		flex: 1;
	}
	.tabs {
		display: flex;
		justify-content: space-between;
		margin: 0 32px;
		margin-bottom: -20px;
		z-index: 1;
	}
	.tabs img {
		display: block;
	}
	.tab,
	.tab_active {
		border-radius: 50%;
		padding: 4px;
		width: 40px;
		box-sizing: border-box;
	}
	.tab img {
		background-color: var(--neutral-7);
	}
	.tab img,
	.tab_active img {
		width: 100%;
		height: 100%;
		box-sizing: border-box;
		border-radius: 50%;
		padding: 20%;
	}
	.tab img {
		background-color: var(--neutral-7);
	}
	.tab-1,
	.tab_content-1 {
		background: var(--gradient-blue);
	}
	.tab-2,
	.tab_content-2 {
		background: var(--gradient-red);
	}
	.tab-3,
	.tab_content-3 {
		background: var(--gradient-yellow);
	}
	.tab_content {
		display: none;
	}
	.tab_content_active {
		border-radius: 20px;
		padding: 4px;
		flex: 1;
	}
	.tab_content-text {
		box-sizing: border-box;
		border-radius: 16px;
		background-color: var(--neutral-7);
		padding: 32px 16px 16px 24px;
		height: 100%;
	}
	.tab_content-heading,
	.tab_content-body {
		margin: 0;
	}
	.tab_content-heading {
		font: var(--big);
	}
	.tab_content-body {
		font: var(--medium);
		margin-top: 8px;
		margin-left: 8px;
	}
	.testimonials {
		height: 400px;
		padding: 40px 20px;
		display: flex;
		flex-direction: column;
		gap: 32px;
		box-sizing: border-box;
	}
	.testimonials_heading {
		font: var(--bigger);
		text-align: center;
	}
	.testimonials_container {
		display: flex;
	}
	.btn-left,
	.btn-right {
		height: fit-content;
		border: none;
		background: none;
		align-self: center;
	}
	.btn-left img,
	.btn-right img {
		width: 12px;
		height: 24px;
	}
	.testimonials_slides {
		overflow: hidden;
		display: flex;
	}
	.testimonial {
		flex: 0 0 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		text-align: center;
		transition: transform 0.25s ease-in-out;
	}
	.testimonial_photo {
		border: 4px solid var(--neutral-6);
		border-radius: 50%;
		width: 64px;
	}
	.testimonial_name {
		font: var(--big);
		margin: 16px 0px;
	}
	.testimonial_text {
		font: var(--medium);
		margin: 0px 16px;
	}
	.download {
		background: var(--gradient-blue);
		height: 240px;
		display: flex;
		flex-direction: column;
		padding: 48px 24px;
		box-sizing: border-box;
		justify-content: space-between;
	}
	.download_heading {
		font: var(--bigger);
		color: var(--neutral-7);
		text-align: center;
	}
	.download_links {
		display: flex;
		width: 240px;
		align-self: center;
		gap: 40px;
	}
	.download_links a {
		flex: 1;
	}
	.download_links img {
		width: 100%;
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
		text-decoration: underline;
		font: var(--body);
		color: var(--neutral-3);
		display: inline;
	}

	@media screen and (min-width: 500px) {
		header {
			padding: 35px 16px;
		}
		ul {
			height: 45px;
			gap: 12px;
		}
		.signup-div {
			padding: 3px;
			border-radius: 75px;
		}
		.signup {
			border-radius: 75px;
			padding: 6px 12px;
		}
		.hero {
			height: 360px;
		}
		:global(.hero-cta) {
			bottom: -36px;
			box-shadow: 0 6px 6px 6px rgba(0, 0, 0, 0.2);
		}
		.features {
			height: 600px;
			padding: 60px 30px;
			align-items: center;
		}
		.tabs_container {
			width: 80%;
		}
		.tabs {
			margin: 0 48px;
			margin-bottom: -30px;
		}
		.tab,
		.tab_active {
			padding: 6px;
			width: 60px;
		}
		.tab_content_active {
			border-radius: 30px;
			padding: 6px;
		}
		.tab_content-text {
			border-radius: 24px;
			padding: 48px 24px 24px 36px;
			height: 100%;
		}
		.tab_content-body {
			margin-top: 16px;
			margin-left: 24px;
		}
		.testimonials {
			height: 600px;
			padding: 60px 30px;
			gap: 48px;
			align-items: center;
		}
		.testimonials_container {
			width: 80%;
		}
		.btn-left img,
		.btn-right img {
			width: 16px;
			height: 36px;
		}
		.testimonial_photo {
			border: 6px solid var(--neutral-6);
			width: 96px;
		}
		.testimonial_name {
			margin: 24px 0px;
		}
		.testimonial_text {
			margin: 0px 24px;
		}
		.download {
			height: 360px;
			padding: 36px 16px;
		}
		.download_links {
			width: 360px;
			gap: 60px;
		}
		footer {
			padding: 16px 48px;
		}
		.footer_hr {
			border: 1px solid var(--neutral-5);
			margin: 12px -16px;
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
		.signup-div {
			padding: 4px;
			border-radius: 100px;
		}
		.signup {
			border-radius: 100px;
			padding: 8px 16px;
		}
		.hero {
			height: 480px;
		}
		:global(.hero-cta) {
			bottom: -48px;
			box-shadow: 0 8px 8px 8px rgba(0, 0, 0, 0.2);
		}
		.features {
			height: 800px;
			padding: 80px 40px;
			align-items: center;
		}
		.tabs_container {
			width: 50%;
		}
		.tabs {
			margin: 0 64px;
			margin-bottom: -40px;
		}
		.tab,
		.tab_active {
			padding: 8px;
			width: 80px;
		}
		.tab_content_active {
			border-radius: 40px;
			padding: 8px;
		}
		.tab_content-text {
			border-radius: 32px;
			padding: 64px 32px 32px 48px;
			height: 100%;
		}
		.tab_content-body {
			margin-top: 32px;
			margin-left: 32px;
		}
		.testimonials {
			height: 800px;
			padding: 80px 40px;
			gap: 64px;
			align-items: center;
		}
		.testimonials_container {
			width: 50%;
		}
		.btn-left img,
		.btn-right img {
			width: 24px;
			height: 48px;
		}
		.testimonial_photo {
			border: 8px solid var(--neutral-6);
			width: 128px;
		}
		.testimonial_name {
			margin: 32px 0px;
		}
		.testimonial_text {
			margin: 0px 32px;
		}
		.download {
			height: 480px;
			padding: 48px 24px;
		}
		.download_links {
			width: 480px;
			gap: 80px;
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
