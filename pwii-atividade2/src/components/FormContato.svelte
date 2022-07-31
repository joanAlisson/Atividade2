<script>
    import {createEventDispatcher} from 'svelte';

    let nome = '';
    let telefone = '';

    const dispatch = createEventDispatcher();

    const adicionarContato = (e) => {

        if (nome.trim() === '' || telefone.trim() === '') {
            return;
        }



        dispatch('novo-contato', {
            nome,
            telefone
        });

        nome = '';
        telefone = '';
    };


</script>

<main>
    
</main>

<style>
</style>
