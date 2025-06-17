<script>
	import { dicionario } from '$lib/dicionario';
	import { page } from '$app/stores';
	import { goto } from '$app/navigation';

	let termoEncontrado;

	$: {
		const { palavra } = $page.params;
		termoEncontrado = dicionario.find(t => t.palavra === palavra);
	}

	function voltarLista() {
		goto('/dicionario'); // volta para a lista de palavras
	}
</script>

<style>
	button.voltar {
		display: block;
		margin: 2rem auto; /* centraliza horizontalmente */
		padding: 0.5rem 1.5rem;
		font-size: 1rem;
		cursor: pointer;
	}
</style>

{#if termoEncontrado}
	<h2>{termoEncontrado.palavra}</h2>
	<ul>
		{#each termoEncontrado.definicoes as definicao}
			<li>{definicao}</li>
		{/each}
	</ul>
{:else}
	<h2>Palavra não encontrada.</h2>
{/if}

<button class="voltar" on:click={voltarLista}>← Voltar para lista</button>
