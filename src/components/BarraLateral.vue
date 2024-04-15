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
        <nav class="panel mt-">
            <ul>
                <li>
                    <router-link to="/" class="link">
                        <i class="fas fa-tasks" ></i>
                        tarefas
                    </router-link>
                </li>
                <li>
                    <router-link to="/projetos" class="link">
                        <i class="fas fa-project-diagram"></i>
                        projetos
                    </router-link>
                </li>
            </ul>
        </nav>
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

.panel li {
    margin: 8px 0;
}
.link {
    color: #fff;
}
.link:hover {
    color: #FAF0CA;
}
.link.router-link-active {
    color: #FAF0CA;
}

@media only screen and (max-width: 768px) {
    header {
        padding: 2.5rem;
        height: auto;
    }
}
</style>