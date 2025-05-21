<script>
  let unidadeOriginal = '';
  let unidadeConvertida = '';
  let valorOriginal = 0;
  let valorConvertido = 0;
  let tab = 'distancia'; 

 
  function converter() {
    let valor = valorOriginal;

    
    valorConvertido = 0;

    if (tab === 'distancia') {
      if (unidadeOriginal === 'km' && unidadeConvertida === 'm') {
        valorConvertido = valor * 1000;
      } else if (unidadeOriginal === 'm' && unidadeConvertida === 'km') {
        valorConvertido = valor / 1000;
      } else if (unidadeOriginal === 'cm' && unidadeConvertida === 'm') {
        valorConvertido = valor / 100;
      } else if (unidadeOriginal === 'm' && unidadeConvertida === 'cm') {
        valorConvertido = valor * 100;
      } else {
        valorConvertido = 'Conversão não suportada';
      }
    } else if (tab === 'peso') {
      if (unidadeOriginal === 'kg' && unidadeConvertida === 'g') {
        valorConvertido = valor * 1000;
      } else if (unidadeOriginal === 'g' && unidadeConvertida === 'kg') {
        valorConvertido = valor / 1000;
      } else if (unidadeOriginal === 'lb' && unidadeConvertida === 'kg') {
        valorConvertido = valor * 0.453592;
      } else if (unidadeOriginal === 'kg' && unidadeConvertida === 'lb') {
        valorConvertido = valor / 0.453592;
      } else {
        valorConvertido = 'Conversão não suportada';
      }
    } else if (tab === 'temperatura') {
      if (unidadeOriginal === 'C' && unidadeConvertida === 'F') {
        valorConvertido = (valor * 9/5) + 32;
      } else if (unidadeOriginal === 'F' && unidadeConvertida === 'C') {
        valorConvertido = (valor - 32) * 5/9;
      } else if (unidadeOriginal === 'C' && unidadeConvertida === 'K') {
        valorConvertido = valor + 273.15;
      } else if (unidadeOriginal === 'K' && unidadeConvertida === 'C') {
        valorConvertido = valor - 273.15;
      } else {
        valorConvertido = 'Conversão não suportada';
      }
    } else if (tab === 'tempo') {
      if (unidadeOriginal === 's' && unidadeConvertida === 'min') {
        valorConvertido = valor / 60;
      } else if (unidadeOriginal === 'min' && unidadeConvertida === 's') {
        valorConvertido = valor * 60;
      } else if (unidadeOriginal === 'min' && unidadeConvertida === 'h') {
        valorConvertido = valor / 60;
      } else if (unidadeOriginal === 'h' && unidadeConvertida === 'min') {
        valorConvertido = valor * 60;
      } else if (unidadeOriginal === 's' && unidadeConvertida === 'h') {
        valorConvertido = valor / 3600;
      } else if (unidadeOriginal === 'h' && unidadeConvertida === 's') {
        valorConvertido = valor * 3600;
      } else {
        valorConvertido = 'Conversão não suportada';
      }
    } else if (tab === 'area') {
      
      if (unidadeOriginal === 'm²' && unidadeConvertida === 'cm²') {
        valorConvertido = valor * 10000;
      } else if (unidadeOriginal === 'cm²' && unidadeConvertida === 'm²') {
        valorConvertido = valor / 10000;
      } else if (unidadeOriginal === 'km²' && unidadeConvertida === 'm²') {
        valorConvertido = valor * 1000000;
      } else if (unidadeOriginal === 'm²' && unidadeConvertida === 'km²') {
        valorConvertido = valor / 1000000;
      } else if (unidadeOriginal === 'acre' && unidadeConvertida === 'm²') {
        valorConvertido = valor * 4046.86;
      } else if (unidadeOriginal === 'm²' && unidadeConvertida === 'acre') {
        valorConvertido = valor / 4046.86;
      } else if (unidadeOriginal === 'ha' && unidadeConvertida === 'm²') {
        valorConvertido = valor * 10000;
      } else if (unidadeOriginal === 'm²' && unidadeConvertida === 'ha') {
        valorConvertido = valor / 10000;
      } else {
        valorConvertido = 'Conversão não suportada';
      }
    } else if (tab === 'volume') {
     
      if (unidadeOriginal === 'l' && unidadeConvertida === 'ml') {
        valorConvertido = valor * 1000;
      } else if (unidadeOriginal === 'ml' && unidadeConvertida === 'l') {
        valorConvertido = valor / 1000;
      } else if (unidadeOriginal === 'm³' && unidadeConvertida === 'l') {
        valorConvertido = valor * 1000;
      } else if (unidadeOriginal === 'l' && unidadeConvertida === 'm³') {
        valorConvertido = valor / 1000;
      } else if (unidadeOriginal === 'gal' && unidadeConvertida === 'l') {
        valorConvertido = valor * 3.78541;
      } else if (unidadeOriginal === 'l' && unidadeConvertida === 'gal') {
        valorConvertido = valor / 3.78541;
      } else {
        valorConvertido = 'Conversão não suportada';
      }
    } else {
      valorConvertido = 'Selecione uma aba válida';
    }
  }

  
  function resetConversion() {
    valorOriginal = 0;
    unidadeOriginal = '';
    unidadeConvertida = '';
    valorConvertido = 0;
  }

  
  function changeTab(newTab) {
    tab = newTab;
    resetConversion();
  }
</script>

<main>
  <div class="container">
    <h1>Conversor de Unidades</h1>

    <div class="tabs">
      <button on:click={() => changeTab('distancia')}>Distância</button>
      <button on:click={() => changeTab('peso')}>Peso</button>
      <button on:click={() => changeTab('temperatura')}>Temperatura</button>
      <button on:click={() => changeTab('tempo')}>Tempo</button>
      <button on:click={() => changeTab('area')}>Área</button>
      <button on:click={() => changeTab('volume')}>Volume</button>
    </div>

    {#if tab === 'distancia'}
      <h2>Distância</h2>
      <input type="number" bind:value={valorOriginal} placeholder="Valor Original" />
      <select bind:value={unidadeOriginal} class="unit-select">
        <option value="">Selecione a unidade original</option>
        <option value="km">Km</option>
        <option value="m">Metros</option>
        <option value="cm">Centímetros</option>
      </select>
      <select bind:value={unidadeConvertida} class="unit-select">
        <option value="">Selecione a unidade convertida</option>
        <option value="km">Km</option>
        <option value="m">Metros</option>
        <option value="cm">Centímetros</option>
      </select>
      <button on:click={converter}>Converter</button>
      <p>Valor Convertido: {valorConvertido}</p>
    {/if}

    {#if tab === 'peso'}
      <h2>Peso</h2>
      <input type="number" bind:value={valorOriginal} placeholder="Valor Original" />
      <select bind:value={unidadeOriginal} class="unit-select">
        <option value="">Selecione a unidade original</option>
        <option value="kg">Kg</option>
        <option value="g">Gramas</option>
        <option value="lb">Libras</option>
      </select>
      <select bind:value={unidadeConvertida} class="unit-select">
        <option value="">Selecione a unidade convertida</option>
        <option value="kg">Kg</option>
        <option value="g">Gramas</option>
        <option value="lb">Libras</option>
      </select>
      <button on:click={converter}>Converter</button>
      <p>Valor Convertido: {valorConvertido}</p>
    {/if}

    {#if tab === 'temperatura'}
      <h2>Temperatura</h2>
      <input type="number" bind:value={valorOriginal} placeholder="Valor Original" />
      <select bind:value={unidadeOriginal} class="unit-select">
        <option value="">Selecione a unidade original</option>
        <option value="C">Celsius</option>
        <option value="F">Fahrenheit</option>
        <option value="K">Kelvin</option>
      </select>
      <select bind:value={unidadeConvertida} class="unit-select">
        <option value="">Selecione a unidade convertida</option>
        <option value="C">Celsius</option>
        <option value="F">Fahrenheit</option>
        <option value="K">Kelvin</option>
      </select>
      <button on:click={converter}>Converter</button>
      <p>Valor Convertido: {valorConvertido}</p>
    {/if}

    {#if tab === 'tempo'}
      <h2>Tempo</h2>
      <input type="number" bind:value={valorOriginal} placeholder="Valor Original" />
      <select bind:value={unidadeOriginal} class="unit-select">
        <option value="">Selecione a unidade original</option>
        <option value="s">Segundos</option>
        <option value="min">Minutos</option>
        <option value="h">Horas</option>
      </select>
      <select bind:value={unidadeConvertida} class="unit-select">
        <option value="">Selecione a unidade convertida</option>
        <option value="s">Segundos</option>
        <option value="min">Minutos</option>
        <option value="h">Horas</option>
      </select>
      <button on:click={converter}>Converter</button>
      <p>Valor Convertido: {valorConvertido}</p>
    {/if}

    {#if tab === 'area'}
      <h2>Área</h2>
      <input type="number" bind:value={valorOriginal} placeholder="Valor Original" />
      <select bind:value={unidadeOriginal} class="unit-select">
        <option value="">Selecione a unidade original</option>
        <option value="m²">Metros Quadrados</option>
        <option value="cm²">Centímetros Quadrados</option>
        <option value="km²">Kilômetros Quadrados</option>
        <option value="acre">Acres</option>
        <option value="ha">Hectares</option>
      </select>
      <select bind:value={unidadeConvertida} class="unit-select">
        <option value="">Selecione a unidade convertida</option>
        <option value="m²">Metros Quadrados</option>
        <option value="cm²">Centímetros Quadrados</option>
        <option value="km²">Kilômetros Quadrados</option>
        <option value="acre">Acres</option>
        <option value="ha">Hectares</option>
      </select>
      <button on:click={converter}>Converter</button>
      <p>Valor Convertido: {valorConvertido}</p>
    {/if}

    {#if tab === 'volume'}
      <h2>Volume</h2>
      <input type="number" bind:value={valorOriginal} placeholder="Valor Original" />
      <select bind:value={unidadeOriginal} class="unit-select">
        <option value="">Selecione a unidade original</option>
        <option value="l">Litros</option>
        <option value="ml">Mililitros</option>
        <option value="m³">Metros Cúbicos</option>
        <option value="gal">Galões</option>
      </select>
      <select bind:value={unidadeConvertida} class="unit-select">
        <option value="">Selecione a unidade convertida</option>
        <option value="l">Litros</option>
        <option value="ml">Mililitros</option>
        <option value="m³">Metros Cúbicos</option>
        <option value="gal">Galões</option>
      </select>
      <button on:click={converter}>Converter</button>
      <p>Valor Convertido: {valorConvertido}</p>
    {/if}
  </div>
</main>

<style>
  .container {
    background-color: #fff;
    padding: 30px;
    border-radius: 10px;
    border: 2px solid #6a0dad;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
    width: 350px;
    text-align: center;
  }

  h1, h2 {
    color: #6a0dad;
  }

  .tabs button {
    margin: 5px;
    background-color: #6a0dad;
    color: white;
    padding: 10px 10px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
  }

  .tabs button:hover {
    background-color: #4b0082;
  }

  input {
    margin: 10px;
    padding: 10px;
    border: 1px solid #6a0dad;
    border-radius: 5px;
    width: 200px;
  }

  
  select.unit-select {
    margin: 10px;
    padding: 10px;
    border: 1px solid #6a0dad; 
    border-radius: 5px;
    width: 200px;
    background-color: #fff; 
    color: #6a0dad; 
    font-size: 16px;
    cursor: pointer;
  }

  
  select.unit-select option {
    background-color: #fff; 
    color: #6a0dad; 
  }

  
  select.unit-select:focus {
    border-color: #6a0dad;
    outline: none;
    background-color: #f5f5f5; 
  }

  button {
    margin: 10px;
    padding: 10px 20px;
    background-color: #6a0dad;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
  }

  button:hover {
    background-color: #4b0082;
  }

  p {
    font-size: 1.2em;
    color: #6a0dad;
  }
</style>

