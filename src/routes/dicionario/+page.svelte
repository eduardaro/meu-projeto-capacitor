<script>
	import { dicionario } from '$lib/dicionario';

	let palavra = $state('');
	let filtradas = $state(dicionario);

	function buscar() {
		if (palavra == '') {
			filtradas = dicionario;
			return;
		}

		filtradas = [];
		for (const termo of dicionario) {
			if (termo.palavra.startsWith(palavra)) {
				filtradas.push(termo);
			}
		}
	}
</script>

<div>
	<input placeholder="digite uma palavra" oninput={buscar} bind:value={palavra} />
</div>
<div>
	<ul>
		{#each filtradas as termo}
			<li><a href="/dicionario/{termo.palavra}">{termo?.palavra}</a></li>
		{/each}
	</ul>
</div>
