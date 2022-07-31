<script>
 

    let contatos = [];

    $: numContatos = contatos.length;
    $: posicao = -1

    const salvarContato = (event) => {

        if(posicao != -1){
            contatos[posicao].nome = document.getElementById("nome").value
            contatos[posicao].telefone = document.getElementById("telefone").value
            posicao = -1
        } else {
            contatos = [...contatos, {
                nome: document.getElementById("nome").value,
                telefone: document.getElementById("telefone").value
            }]
        }

        document.getElementById("nome").value  = ""
        document.getElementById("telefone").value = ""

    };

    const excluirContato = (idx) => {
        let copy = [...contatos];
        copy.splice(idx, 1);
        contatos = copy;

    };

    const editarContato = (idx) => {

        document.getElementById("nome").value  = contatos[idx].nome
        document.getElementById("telefone").value = contatos[idx].telefone
        posicao = idx
    };
</script>

<main>
    <h1>Agenda Svelte</h1>

    <hr>

    <div class="form-contato form-group">
        <p>
            <input placeholder="Nome" type="text" name="nome" id="nome"  class="form-control"
                    />
        </p>
        <p>
            <input placeholder="Telefone" name="telefone" id="telefone"  class="form-control"
                    />
        </p>
        <button on:click={salvarContato} type="submit" class="btn btn-primary">
            Salvar
        </button>

    </div>

    <div class="list-group">
        {#if numContatos <= 0}
            <p>Adicione um contato na agenda...</p>
        {:else}
            <p>Há {numContatos} contatos na agenda.</p>
        {/if}

        {#each contatos as contato, index}
            <div class="list-group-item">
                <span class="nome_class">Nome: <strong>{ contato.nome }</strong></span>
                <p>
                    <span class="telefone_class">
                        Telefone: <strong>{ contato.telefone }</strong>
                    </span>
                </p>
                <div>
                    <button title="Excluir"
                            on:click={() => excluirContato(index)}>
                        Excluir
                    </button>
                    <button title="Editar"
                            on:click={() => editarContato(index)}>
                        Editar
                    </button>
                </div>
            </div>
        {/each}

     </div>

     <hr />
</main>

<style>
    .nome_class {
        margin-top: 3px;
    }
</style>
