<script>
	let display = '';

	function backspace() {
		display = display.length;
	}
</script>

<div class="container">
	<center><h1>❌Bem Vindos ao Jogo da Velha⭕</h1></center>
	<div class="text-center mt-3">
		<table class="table table-borderless">
			<tbody>
				<tr>
					<td><input type="text" placeholder="x/o" span class="border border-3" /></td>
					<td><input type="text" placeholder="x/o" span class="border border-3" /></td>
					<td><input type="text" placeholder="x/o" /></td>
				</tr>

				<tr>
					<td><input type="text" placeholder="x/o" span class="border border-3" /></td>
					<td><input type="text" placeholder="x/o" span class="border border-3" /></td>
					<td><input type="text" placeholder="x/o" span class="border border-3" /></td>
				</tr>

				<tr>
					<td><input type="text" placeholder="x/o" span class="border border-3" /></td>
					<td><input type="text" placeholder="x/o" span class="border border-3" /></td>
					<td><input type="text" placeholder="x/o" span class="border border-3" /></td>
				</tr>
			</tbody>
		</table>
	</div>
	<button class="backspace" onclick={() => backspace()}>⭮Reiniciar</button>
</div>

<style>
	.container {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		min-height: 100vh;
		background: linear-gradient(145deg, #e9d8fd, #fbe4ff);
		padding: 1rem;
		text-align: center;
		color: #5e3c6d;
	}

	h1 {
		font-size: 4rem;
		color: #a64ac9;
		margin-bottom: 1rem;
	}
</style>
