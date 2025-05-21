<script>
    // Função para gerar senha aleatória
    let passwordLength = 12;
    let passwordCount = 1;
    let includeLowerCase = true;
    let includeUpperCase = true;
    let includeNumbers = true;
    let includeSpecialChars = true;
    
    const lowerCaseChars = 'abcdefghijklmnopqrstuvwxyz';
    const upperCaseChars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
    const numbers = '0123456789';
    const specialChars = '!@#$%^&*()_-+=<>?';
  
    function generatePassword() {
      let characters = '';
      let password = '';
  
      if (includeLowerCase) characters += lowerCaseChars;
      if (includeUpperCase) characters += upperCaseChars;
      if (includeNumbers) characters += numbers;
      if (includeSpecialChars) characters += specialChars;
  
      if (!characters) return ''; // Caso nenhuma opção esteja selecionada
  
      for (let i = 0; i < passwordLength; i++) {
        password += characters.charAt(Math.floor(Math.random() * characters.length));
      }
      return password;
    }
  
    function generateMultiplePasswords() {
      let passwords = [];
      for (let i = 0; i < passwordCount; i++) {
        passwords.push(generatePassword());
      }
      return passwords;
    }
  
    function copyToClipboard(password) {
      navigator.clipboard.writeText(password).then(() => {
        alert('Senha copiada para a área de transferência!');
      }).catch((err) => {
        console.error('Erro ao copiar a senha: ', err);
      });
    }
  
    let passwords = generateMultiplePasswords();
  </script>
  
  <div class="bd">
    <h1>Gerador de Senhas</h1>
  
    <div class="input-group">
      <label for="passwordLength">Comprimento da senha:</label>
      <input type="range" id="passwordLength" bind:value={passwordLength} min="4" max="32" style= "accent-color:#6719bb"/>
      <p>Tamanho: {passwordLength}</p>
    </div>
  
    <div class="input-group">
      <label for="passwordCount">Número de senhas:</label>
      <input type="number" id="passwordCount" bind:value={passwordCount} min="1" max="10" />
    </div>
  
    <div class="checkbox-group">
      <label>
        <input type="checkbox" bind:checked={includeLowerCase} /> Incluir letras minúsculas
      </label>
      <label>
        <input type="checkbox" bind:checked={includeUpperCase} /> Incluir letras maiúsculas
      </label>
      <label>
        <input type="checkbox" bind:checked={includeNumbers} /> Incluir números
      </label>
      <label>
        <input type="checkbox" bind:checked={includeSpecialChars} /> Incluir caracteres especiais
      </label>
    </div>
  
    <button on:click={() => passwords = generateMultiplePasswords()}>Gerar Senhas</button>
  
    {#if passwords.length > 0}
      <h2>Senhas Geradas:</h2>
      <ul>
        {#each passwords as password}
          <li>
            {password} 
            <button on:click={() => copyToClipboard(password)}>Copiar</button>
          </li>
        {/each}
      </ul>
    {/if}
    </div>
  
  <style>
  
    .bd {
      background-color: #7131b9ce;
      color: white;
      padding: 20px;
      align-items: center;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      text-align: center;
      max-width: 400px;
      width: 100%;
      justify-content: center;
      flex-direction: column;
    }
  
    h1 {
      font-size: 2rem;
      margin-bottom: 20px;
    }
  
    h2 {
      font-size: 1.5rem;
      margin-top: 20px;
      margin-bottom: 15px;
    }
  
    .input-group {
      margin-bottom: 15px;
    }
  
    .input-group input {
      padding: 8px;
      margin-top: 5px;
      width: 100%;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
  
    .checkbox-group {
      margin-bottom: 20px;
    }
  
    .checkbox-group label {
      display: block;
      margin: 5px 0;
    }
  
    button {
      padding: 10px 20px;
      background-color: #9f73dd;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      margin-top: 10px;
    }
  
    button:hover {
      background-color: #c583f8;
    }
  
    ul {
      list-style-type: none;
      padding: 0;
      align-items: center;
      margin: 0 auto;
    }
  
    li {
      background-color: #6719bb;
      margin: 10px 0;
      padding: 10px;
      border-radius: 5px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
  
    li button {
      background-color: #ffffff;
      color: rgb(0, 0, 0);
      padding: 5px 10px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
  
    li button:hover {
      background-color: #cca3e4;
    }
  </style>
  