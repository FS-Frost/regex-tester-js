<script lang="ts">
	import { event } from '../lib/regex/ass.json';
	let regex: string = event;
	let input: string = 'abcDialogue: 0,0:00:23.47,0:00:25.37,Default,KuroNe,0,0,0,,Mis felicidades.';
	let errorMsg: string = '';

	$: regexResult = applyRegex(regex, input);
	$: groups = regexResult?.groups ?? {};
	$: groupKeys = Object.keys(groups);
	$: capture = regexResult?.[0] ?? '';
	$: preCapture = input.substring(0, regexResult?.index ?? 0);
	$: postCapture = input.substring(preCapture.length + capture.length);
	$: success = errorMsg.length == 0;

	function applyRegex(regex: string, input: string): RegExpExecArray | null {
		let result: RegExpExecArray | null = null;
		errorMsg = '';

		try {
			const exp = RegExp(regex);
			result = exp.exec(input);
		} catch (error) {
			const msg = 'ERROR: applying regex: ';
			console.error(msg, error);
			errorMsg = `${msg} ${error}`;
			return null;
		}

		if (result == null) {
			console.info('No matches');
			return null;
		}

		console.log({ result });

		if (result.length == 0) {
			console.info('No captures');
			return null;
		}

		return result;
	}
</script>

<div class="regex-tester">
	<div class="regex">
		<label for="regex">Regular Expression</label>
		<textarea class="textarea" bind:value={regex} />
	</div>

	<div class="capture">
		{preCapture}<span>{capture}</span>{postCapture}
	</div>

	<div class="text-input">
		<label for="text-input">Input</label>
		<textarea class="textarea" bind:value={input} />
	</div>

	{#if !success}
		<div class="error">
			<p class="has-text-danger">{errorMsg}</p>
		</div>
	{:else}
		<div class="table-container">
			<table class="table is-striped is-fullwidth">
				<thead>
					<tr>
						<th>Capture</th>
						{#each groupKeys as key}
							<th>{key}</th>
						{/each}
					</tr>
				</thead>
				<tbody>
					<tr>
						<td>{regexResult?.[0] ?? ''}</td>
						{#each groupKeys as key}
							<td>{groups[key]}</td>
						{/each}
					</tr>
				</tbody>
			</table>
		</div>
	{/if}
</div>

<style>
	.regex-tester {
		width: 100%;
	}

	label {
		font-weight: bold;
	}

	textarea {
		width: 100%;
		height: 5rem;
	}

	.capture {
		color: darkgray;
		margin-bottom: 0.5rem;
	}

	.capture span {
		color: black;
	}
</style>
