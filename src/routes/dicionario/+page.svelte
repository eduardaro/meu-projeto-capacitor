<script>
	import { dicionario } from '$lib/dicionario';

	let palavra = '';
	let filtradas = dicionario;

	let letraSelecionada = '';

	let palavraDoDia = JSON.parse(localStorage.getItem('palavraDoDia'));
	if (!palavraDoDia) {
		const indiceAleatorio = Math.floor(Math.random() * dicionario.length);
		palavraDoDia = dicionario[indiceAleatorio];
		localStorage.setItem('palavraDoDia', JSON.stringify(palavraDoDia));
	}

	function buscar() {
		if (palavra.trim() === '') {
			filtradas = letraSelecionada
				? dicionario.filter(p => p.palavra.startsWith(letraSelecionada.toLowerCase()))
				: dicionario;
		} else {
			filtradas = dicionario.filter(p => p.palavra.toLowerCase().startsWith(palavra.toLowerCase()));
		}
	}

	function filtrarPorLetra(letra) {
		letraSelecionada = letra;
		palavra = '';
		filtradas = dicionario.filter(p => p.palavra.startsWith(letra.toLowerCase()));
	}
</script>

<style>
	.container {
		max-width: 700px;
		width: 100%;
		background: white;
		border-radius: 8px;
		box-shadow: 0 4px 12px rgb(0 0 0 / 0.1);
		padding: 25px 30px;
	}

	h2 {
		font-weight: 700;
		color: #4c2683;
		margin-bottom: 15px;
	}

	.palavra-dia {
		background: #e8d8ff;
		border: 1px solid #b19cd9;
		padding: 12px 18px;
		border-radius: 6px;
		margin-bottom: 25px;
		text-align: center;
		font-weight: 700;
		font-size: 20px;
	}

	.palavra-dia a {
		color:rgb(3, 0, 9);
		text-decoration: none;
	}

	.palavra-dia a:hover {
		text-decoration: underline;
	}

	input[type="text"] {
		width: 100%;
		padding: 10px 15px;
		font-size: 16px;
		border: 2px solid #cdb6f0;
		border-radius: 6px;
		transition: border-color 0.2s;
		box-sizing: border-box;
		margin-bottom: 20px;
		color: #4c2683;
		background-color: #faf5ff;
	}

	input[type="text"]:focus {
		border-color: #6a4caa;
		outline: none;
		box-shadow: 0 0 5px #9e7bff;
	}

	.az-nav {
		display: flex;
		flex-wrap: wrap;
		gap: 6px;
		justify-content: center;
		margin-bottom: 15px;
	}

	.az-nav button {
		background: #f1eaff;
		border: 1px solid #b19cd9;
		color: #6a4caa;
		padding: 5px 9px;
		font-size: 14px;
		min-width: 30px;
		border-radius: 5px;
		font-weight: 600;
		cursor: pointer;
		transition: all 0.25s ease;
		text-align: center;
	}

	.az-nav button:hover:not(.active) {
		background: #6a4caa;
		border-color: #6a4caa;
		color: white;
	}

	.az-nav button.active {
		background: #4c2683;
		border-color: #4c2683;
		color: white;
		cursor: default;
	}

	.az-box {
		border: 2px solid #b19cd9;
		background-color: #f7f1ff;
		padding: 20px;
		border-radius: 10px;
		max-width: 100%;
		margin-bottom: 25px;
		box-shadow: 0 4px 8px rgb(177 156 217 / 0.3);
	}

	ul {
		list-style: none;
		padding: 0;
		margin-top: 10px;
		display: grid;
		grid-template-columns: repeat(2, 1fr);
		gap: 12px 30px;
	}

	li a {
		text-decoration: none;
		color: black;
		font-weight: 600;
		transition: color 0.3s;
	}

	li a:hover {
		color: #9e7bff;
	}
</style>

<div class="container">
	<div class="palavra-dia">
		<h2>Palavra Aleatória do Dia:</h2>
		<a href={`/dicionario/${palavraDoDia?.palavra}`}><strong>{palavraDoDia?.palavra}</strong></a>
	</div>

	<input
		type="text"
		placeholder="Digite uma palavra"
		bind:value={palavra}
		on:input={buscar} />

	<div class="az-nav">
		{#each 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('') as letra}
			<button
				class:active={letraSelecionada === letra}
				on:click={() => filtrarPorLetra(letra)}>
				{letra}
			</button>
		{/each}
		<button
			on:click={() => {
				letraSelecionada = '';
				filtradas = dicionario;
				palavra = '';
			}}>
			Todos
		</button>
	</div>

	<div class="az-box">
		<ul>
			{#each filtradas as termo}
				<li><a href={`/dicionario/${termo.palavra}`}>{termo.palavra}</a></li>
			{/each}
		</ul>
	</div>
</div>
