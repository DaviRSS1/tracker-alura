<script lang="ts">
import { defineComponent } from 'vue';
import { useStore } from '@/store';
import { ALTERA_PROJETO, ADICIONA_PROJETO } from '@/store/tipo-mutacoes';
import { TipoNotificacao } from '@/interfaces/INotificacao';
import useNotificador from '@/hooks/notificador'

export default defineComponent({
    name: 'Formulario',
    props: {
        id: {
            type: String
        }
    },
    mounted () {
        if (this.id) {
            const projeto = this.store.state.projetos.find(proj => proj.id == this.id)
            this.nomeDoProjeto = projeto?.nome || ''
        }
    },
    data() {
        return {
            nomeDoProjeto: '',
        }
    },
    methods: {
        salvar() {
            if (this.id){
                this.store.commit(ALTERA_PROJETO, {
                    id: this.id,
                    nome: this.nomeDoProjeto
                })
            } else {
                this.store.commit(ADICIONA_PROJETO, this.nomeDoProjeto)
            }
            this.notificar(TipoNotificacao.SUCESSO, 'Excelente!', 'O Projeto foi cadastrado com sucesso!')
            this.nomeDoProjeto = ''
            this.$router.push('/projetos')
        }
    },
    setup() {
        const store = useStore()
        const { notificar } = useNotificador()
        return{
            store,
            notificar
        }
    }
})
</script>

<template>
    <section>
        <form @submit.prevent="salvar">
            <div class="field">
                <label for="nomeDoProjeto" class="label">
                    Nome do Projeto
                </label>
                <input type="text" v-model="nomeDoProjeto" class="input" id="nomeDoProjeto"
                    placeholder="Digite o nome do seu projeto">
            </div>
            <div class="field">
                <button class="button" type="submit">
                    Salvar
                </button>
            </div>
        </form>
    </section>
</template>

<style scoped>

.label {
    color: var(--texto-primario)
}

.input {
    background-color: var(--bg-box);
    color: var(--texto-primario)
}

.input::placeholder {
    color: var(--texto-primario)
}
</style>