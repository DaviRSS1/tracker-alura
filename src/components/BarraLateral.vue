<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'BarraLateral',
    data() {
        return{
            modoEscuroAtivo: false
        }
    },
    computed: {
        textoBotao() {
            if(this.modoEscuroAtivo) {
                return 'Desativar modo escuro'
            }
            else {
                return 'Ativar modo escuro'
            }
        }
    },
    methods: {
        alterarTema() {
            this.modoEscuroAtivo = !this.modoEscuroAtivo
            this.$emit('aoAlterarTema', this.modoEscuroAtivo)
        }
    },
    emits: [ 'aoAlterarTema' ]
})
</script>

<template>
    <header>
        <h1>
            <img src="../assets/logo.png" alt="Logo Alura Tracker">
        </h1>
        <button class="button" @click="alterarTema">
            {{ textoBotao }}
        </button>
    </header>
</template>

<style scoped>
header {
    padding: 1rem;
    background: #0d3b66;
    width: 100%;
    height: 100vh;
    text-align:center;
}

.button{
    border: 1px solid var(--texto-primario);
    background-color: var(--bg-primario);
    color: var(--texto-primario);
}

@media only screen and (max-width: 768px) {
    header {
        padding: 2.5rem;
        height: auto;
    }
}
</style>