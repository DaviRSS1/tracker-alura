<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'box'
})
</script>

<template>
    <div class="box has-text-weight-bold box-tarefa">
        <slot></slot>
    </div>
</template>

<style>
.box-tarefa{
    background-color: var(--bg-box);
    color: var(--texto-primario)
}
</style>