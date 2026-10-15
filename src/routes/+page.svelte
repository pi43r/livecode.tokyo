<script module>
	/** @type {Record<string, { default: import('svelte').Component, metadata: { title: string, date: string | Date } }>} */
	const modules = import.meta.glob('/content/posts/*.md', { eager: true });
	const posts = Object.entries(modules)
		.map(([path, post]) => ({
			...post,
			slug: path.split('/').pop()?.replace(/\.md$/, '') ?? '',
			date: new Date(post.metadata.date).toISOString().slice(0, 10)
		}))
		.sort((a, b) => b.date.localeCompare(a.date));
	const description =
		'Livecode Tokyo: meetups, laptop jams, and little notes from the live coding community in Tokyo. Bring your laptop and jam with us :)';
</script>

<svelte:head>
	<title>livecode.tokyo — Livecode Tokyo</title>
	<meta name="description" content={description} />
	<link rel="canonical" href="https://livecode.tokyo/" />
	<meta name="theme-color" content="#0310B7" />
	<meta property="og:type" content="website" />
	<meta property="og:title" content="livecode.tokyo — Livecode Tokyo" />
	<meta property="og:description" content={description} />
	<meta property="og:url" content="https://livecode.tokyo/" />
	<meta property="og:site_name" content="Livecode Tokyo" />
	<meta property="og:image" content="https://livecode.tokyo/lct.jpg" />
	<meta property="og:image:alt" content="The pixel-lettered LCT logo" />
	<meta name="twitter:card" content="summary" />
</svelte:head>

<header id="top" class="flex items-baseline justify-between gap-6 border-b-2 py-5"></header>
<main>
	<section class="pt-12" aria-label="Hello from Livecode Tokyo">
		<div class="overflow-hidden py-6">
			<img
				class="h-auto w-full"
				src="/lct.svg"
				alt="LCT, drawn in delightfully wonky pixel letters"
				width="816"
				height="336"
				fetchpriority="high"
			/>
		</div>
		<div class="flex justify-between gap-6 pt-4 pb-10 text-[clamp(1rem,2vw,1.4rem)]">
			<p>Livecode Tokyo<br />ライブコード東京</p>
			<p class="text-right">bring a laptop.<br />code music.</p>
		</div>
	</section>
	<section
		class="scroll-mt-4 border-t-[6px] border-dotted"
		id="posts"
		aria-labelledby="posts-heading"
	>
		{#each posts as post (post.slug)}
			<article
				id={post.slug}
				aria-label={post.metadata.title}
				class="grid scroll-mt-4 gap-6 border-b-2 border-solid pt-6 pb-10 sm:grid-cols-[minmax(10rem,1fr)_3fr] sm:gap-8 sm:pt-10 sm:pb-14"
			>
				<div
					class="code flex flex-wrap items-start justify-between gap-3 sm:flex-col sm:justify-start"
				>
					<time datetime={post.date}>{post.date.replaceAll('-', '/')}</time>
					<a href={`#${post.slug}`}>{post.metadata.title} ↗</a>
				</div>
				<div class="post-body"><post.default /></div>
			</article>
		{:else}
			<p>Nothing here yet. Our laptops are warming up…</p>
		{/each}
	</section>
</main>
<footer class="flex flex-wrap items-baseline justify-between gap-6 pt-6 pb-12 text-sm">
	<details>
		<summary class="cursor-pointer">what is this place?</summary>
		<p class="mt-4 leading-relaxed">
			A little home for live coding in Tokyo.<br />Laptops, experiments, and good company. Hello,
			World!
		</p>
		<p class="mt-4 leading-relaxed">Organized by Ruiqi, Yifan, Matthias & Benjiemin</p>
	</details>
	<div class="flex gap-2">
		<a href="https://www.instagram.com/livecode.tokyo">instagram</a>
		<a href="#top">back to top ↑</a>
	</div>
</footer>
