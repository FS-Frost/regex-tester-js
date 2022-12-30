<script>
	import github from '$lib/images/github.svg';
	const msgGitHub = 'Fork it on GitHub!';
</script>

<header>
	<corner />
	<h1>Regex Tester JS</h1>
	<corner class="corner">
		<a href="https://github.com/FS-Frost/regex-tester-js" title={msgGitHub}>
			<img src={github} alt={msgGitHub} />
		</a>
	</corner>
</header>

<style>
	header {
		display: flex;
		justify-content: space-between;
	}

	.corner {
		width: 3em;
		height: 3em;
	}

	.corner img {
		width: 4em;
		height: 4em;
		object-fit: contain;
	}
</style>
