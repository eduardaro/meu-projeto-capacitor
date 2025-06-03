<script>
  import { onMount } from 'svelte';
  import Modal from '$lib/components/Modal.svelte';
  import Toast from '$lib/components/Toast.svelte';
  import ToDoList from '$lib/components/ToDoList.svelte';
  import * as bootstrap from 'bootstrap';

  let novaTarefa = $state('');
  let tarefas = $state([]);
  let busca = $state('');
  let filtro = $state('todas');

  let tarefasPendentes = $derived(
    tarefas.filter(tarefa =>
      tarefa.status === 0 &&
      tarefa.conteudo.toLowerCase().includes(busca.toLowerCase())
    )
  );

  let tarefasConcluidas = $derived(
    tarefas.filter(tarefa =>
      tarefa.status === 1 &&
      tarefa.conteudo.toLowerCase().includes(busca.toLowerCase())
    )
  );

  let totalTarefas = $derived(tarefas.length);
  let totalPendentes = $derived(tarefas.filter(t => t.status === 0).length);
  let totalConcluidas = $derived(tarefas.filter(t => t.status === 1).length);

  let conteudoTarefaEditando = $state('');
  let tarefaEditando = $state();
  let tarefaExcluindo;
  let mensagemToast;

  async function adicionarTarefa(event) {
    event.preventDefault();
    novaTarefa = novaTarefa.trim();
    if (!novaTarefa) {
      mensagemToast.show();
      return;
    }
    tarefas.push({ conteudo: novaTarefa, status: 0 });
    novaTarefa = '';
  }

  function editarTarefa(tarefa) {
    tarefaEditando = tarefa;
    conteudoTarefaEditando = tarefa.conteudo;
  }

  function confirmarEdicao() {
    if (!conteudoTarefaEditando.trim()) return;
    tarefaEditando.conteudo = conteudoTarefaEditando;
    tarefaEditando = undefined;
  }

  function cancelarEdicao() {
    tarefaEditando = undefined;
  }

  function excluirTarefa(tarefa) {
    tarefaExcluindo = tarefa;
  }

  function confirmarExclusao() {
    tarefas = tarefas.filter(tarefa => tarefa !== tarefaExcluindo);
    tarefaExcluindo = undefined;
  }

  function alterarStatus(tarefa, status) {
    tarefa.status = status;
  }

  function concluirTodasAsPendentes() {
    tarefas.forEach(tarefa => {
      if (tarefa.status === 0) {
        tarefa.status = 1;
      }
    });
  }

  function reabrirTodasAsConcluidas() {
    tarefas.forEach(tarefa => {
      if (tarefa.status === 1) {
        tarefa.status = 0;
      }
    });
  }

  function setFiltro(novoFiltro) {
    filtro = novoFiltro;
  }

  onMount(() => {
    mensagemToast = new bootstrap.Toast('#mensagemToast');
  });
</script>

<div class="fixed-top pt-5" style="z-index: 1020;">
  <form class="container-fluid input-group px-4 pt-3" onsubmit={adicionarTarefa}>
    <input class="form-control form-control-lg" placeholder="Nova tarefa" bind:value={novaTarefa} />
    <button type="submit" class="btn btn-primary input-group-text" aria-label="adicionar">
      <i class="bi bi-plus-lg"></i>
    </button>
  </form>
  <Toast msg={'Digite algo!'} />
</div>

<div class="container-fluid mt-5 pt-3">
  <!-- Campo de busca -->
  <div class="px-4 mb-3">
    <input
      type="text"
      class="form-control"
      placeholder="Buscar tarefa..."
      bind:value={busca}
    />
  </div>

  <!-- Botão Informações centralizado -->
  <div class="d-flex justify-content-center mb-3">
    <div class="btn-group">
      <button type="button" class="btn btn-dark dropdown-toggle" data-bs-toggle="dropdown" aria-expanded="false" style="width: 1000px;">
        Informações
      </button>
      <ul class="dropdown-menu">
        <!-- Contadores com fundo roxo -->
        <div class="px-4 mb-3">
          <div class="p-3 rounded text-white" style="background-color: #6f42c1;">
            Total: <strong>{totalTarefas}</strong> |
            Pendentes: <strong>{totalPendentes}</strong> |
            Concluídas: <strong>{totalConcluidas}</strong>
          </div>
        </div>
        <div class="d-flex justify-content-between align-items-center mb-3 px-2">
          <h5 class="mb-0">Filtrar tarefas</h5>
          <div class="btn-group">
            <button class="btn btn-sm btn-secondary" onclick={() => setFiltro('todas')}>Todas</button>
            <button class="btn btn-sm btn-primary" onclick={() => setFiltro('pendentes')}>Pendentes</button>
            <button class="btn btn-sm btn-success" onclick={() => setFiltro('concluidas')}>Concluídas</button>
          </div>
        </div>
      </ul>
    </div>
  </div>

  {#if filtro === 'todas' || filtro === 'pendentes'}
    <div class="d-flex justify-content-between align-items-center mb-2 px-2">
      <h5 class="mb-0">Pendentes</h5>
      <button class="btn btn-sm btn-success" onclick={concluirTodasAsPendentes}>
        Marcar todas como concluídas
      </button>
    </div>
    <ToDoList
      tarefas={tarefasPendentes}
      {tarefaEditando}
      bind:conteudoTarefaEditando
      {editarTarefa}
      {confirmarEdicao}
      {cancelarEdicao}
      {alterarStatus}
      {excluirTarefa}
    />
  {/if}

  {#if filtro === 'todas' || filtro === 'concluidas'}
    <hr />
    <div class="d-flex justify-content-between align-items-center mb-2 px-2">
      <h5 class="mb-0">Concluídas</h5>
      <button class="btn btn-sm btn-danger" onclick={reabrirTodasAsConcluidas}>
        Marcar todas como pendentes
      </button>
    </div>
    <ToDoList
      tarefas={tarefasConcluidas}
      {tarefaEditando}
      bind:conteudoTarefaEditando
      {editarTarefa}
      {confirmarEdicao}
      {cancelarEdicao}
      {alterarStatus}
      {excluirTarefa}
    />
  {/if}
</div>

<Modal msg={'Deseja excluir a tarefa?'} acao={confirmarExclusao} />
