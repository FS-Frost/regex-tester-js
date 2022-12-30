<script>
	import RegexTester from './RegexTester.svelte';
</script>

<svelte:head>
	<title>Regex Tester JS</title>
	<meta name="description" content="Regex tester app made with JavaScript" />
</svelte:head>

<section>
	<RegexTester />
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}
</style>
