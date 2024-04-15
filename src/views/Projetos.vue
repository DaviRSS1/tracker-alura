<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'Projetos'
})

</script>

<template>
    <div class="projetos">
        <h1 class="title">Projetos</h1>
        <RouterView></RouterView>
    </div>
</template>

<style scoped>
.projetos {
    color: var(--texto-primario);
    padding: 1.5rem;
    background-color: var(--bg-box)
}

.title {
    color: var(--texto-primario);
}

</style>