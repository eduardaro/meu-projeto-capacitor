<h1> MegaSorte</h1>
<script>
    let numeros = [];
  
    function sortear() {
      const sorteio = new Set();
      while (sorteio.size < 6) {
        const numero = Math.floor(Math.random() * 60) + 1;
        sorteio.add(numero);
      }
      numeros = Array.from(sorteio).sort((a, b) => a - b);
    }
  </script>
  
  <style>
    .container {
      text-align: center;
      padding: 2rem;
      font-family: Arial, sans-serif;
    }
  
    .numeros {
      display: flex;
      justify-content: center;
      gap: 1rem;
      flex-wrap: wrap;
      margin-top: 1rem;
    }
  
    .bola {
      background: #00a859;
      color: white;
      width: 50px;
      height: 50px;
      display: flex;
      justify-content: center;
      align-items: center;
      border-radius: 50%;
      font-size: 1.2rem;
      font-weight: bold;
      box-shadow: 0 2px 5px rgba(0,0,0,0.2);
    }
  
    button {
      background-color: #007bff;
      color: white;
      padding: 0.6rem 1.2rem;
      border: none;
      border-radius: 8px;
      font-size: 1rem;
      cursor: pointer;
      margin-top: 1rem;
    }
  
    button:hover {
      background-color: #0056b3;
    }
  </style>
  
  <div class="container">
    <h1>MegaSorte 🎲</h1>
    <button on:click={sortear}>Sortear Números</button>
  
    {#if numeros.length > 0}
      <div class="numeros">
        {#each numeros as n}
          <div class="bola">{n}</div>
        {/each}
      </div>
    {/if}
  </div>
  