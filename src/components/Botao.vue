<script lang="ts">
import { defineComponent } from 'vue';


export default defineComponent({
    methods: {
        clicado() : void {
            this.$emit('clicado')
        }
    },
    props: {
        desabilitado: { type: Boolean, required: true },
        icon: { type: String, required: true },
        texto: { type: String, required: true }
    },
    emits: [ 'clicado']
}) 
</script>

<template>
    <button class="button" @click="clicado" :disabled="desabilitado">
        <span class="icon">
            <i :class="icon"></i>
        </span>
        <span>{{ texto }}</span>
    </button>
</template>

<style scoped>
.button{
    border: 1px solid var(--texto-primario);
    background-color: var(--bg-primario);
    color: var(--texto-primario);
}
</style>
