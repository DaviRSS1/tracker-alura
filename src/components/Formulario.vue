<script lang="ts">
import { computed, defineComponent } from 'vue';
import Temporizador from './Temporizador.vue';
import { useStore } from 'vuex';
import { key } from '@/store';
import { TipoNotificacao } from '@/interfaces/INotificacao';
import useNotificador from '@/hooks/notificador'

export default defineComponent({
    name: 'Formulario',
    components: {
        Temporizador
    },
    data() {
        return {
            descricao: '',
            idProjeto: ''
        }
    },
    
    methods: {
        finalizarTarefa(tempoDecorrido: number): void {
            const projeto = this.projetos.find((p) => p.id == this.idProjeto);
            if (!projeto) {
                this.notificar(TipoNotificacao.FALHA, 'Ops!', "Selecione um projeto antes de finalizar a tarefa!")
                return;
            }
            this.$emit('aoSalvarTarefa', {
                duracaoEmSegundos: tempoDecorrido,
                descricao: this.descricao,
                projeto: projeto
            })
            this.descricao = ''
        },
    },
    setup() {
        const store = useStore(key)
        const { notificar }  = useNotificador() 
        return {
            projetos: computed(() => store.state.projetos),
            store,
            notificar
        }
    },
    emits: ['aoSalvarTarefa']
})
</script>

<template>
    <div class="box formulario">
        <div class="columns">
            <div class="column is-5" role="form" aria-label="Formulário para criação de uma tarefa">
                <input type="text" class="input" placeholder="Qual tarefa você deseja iniciar?" v-model="descricao">
            </div>
            <div class="column is-3">
                <div class="select">
                    <select v-model="idProjeto" class="selecao">
                        <option value="">Selecione o projeto</option>
                        <option :value="projeto.id" v-for="projeto in projetos" :key="projeto.id">
                            {{ projeto.nome }}
                        </option>
                    </select>
                </div>
            </div>
            <div class="column">
                <Temporizador @ao-temporizador-finalizado="finalizarTarefa" />
            </div>
        </div>
    </div>
</template>

<style>
.formulario {
    color: var(--texto-primario);
    background-color: var(--bg-box)
}

.input {
    background-color: var(--bg-box);
    color: var(--texto-primario)
}

.input::placeholder {
    color: var(--texto-primario)
}

.selecao{
    background-color: var(--bg-box) !important;
    color: var(--texto-primario) !important;
}
</style>