<script>
	import { dicionario } from '$lib/dicionario';


	let palavra = $state('');
	let filtradas = $state(dicionario);

	// Função para selecionar uma palavra aleatória
	function getPalavraAleatoria() {
		const indiceAleatorio = Math.floor(Math.random() * dicionario.length);
		return dicionario[indiceAleatorio];
	}

	// Verifique se a palavra aleatória do dia já foi salva no localStorage
	let palavraDoDia = JSON.parse(localStorage.getItem('palavraDoDia'));

	// Se não houver uma palavra salva, crie uma e armazene no localStorage
	if (!palavraDoDia) {
		palavraDoDia = getPalavraAleatoria();
		localStorage.setItem('palavraDoDia', JSON.stringify(palavraDoDia));
	}

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
	<h2>Palavra Aleatória do Dia:</h2>
	<a href={`/dicionario/${palavraDoDia?.palavra}`}><strong>{palavraDoDia?.palavra}</strong></a>
</div>

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
