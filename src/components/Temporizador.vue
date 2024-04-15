<script lang="ts">
import { defineComponent } from 'vue';
import Cronometro from './Cronometro.vue';
import Botao from './Botao.vue';

export default defineComponent({
    name: 'Temporizador',
    emits: [ 'aoTemporizadorFinalizado' ] ,
    components: {
        Cronometro,
        Botao
    },
    data () {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false,
        }
    },
    methods: {
        iniciar () {
            this.cronometroRodando = true
            this.cronometro = setInterval(() => {
                this.tempoEmSegundos += 1
            }, 1000)
        },
        finalizar() {
            clearInterval(this.cronometro)
            this.cronometroRodando = false
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            this.tempoEmSegundos = 0
        }
    }
})
</script>

<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between ">
        <Cronometro :tempoEmSegundos="tempoEmSegundos" />
        <Botao 
            :desabilitado="cronometroRodando"
            texto="play"
            icon="fas fa-play"
            @clicado="iniciar"
        />
        <Botao 
            :desabilitado="!cronometroRodando"
            texto="stop"
            icon="fas fa-stop"
            @clicado="finalizar"
        />
    </div>
</template>