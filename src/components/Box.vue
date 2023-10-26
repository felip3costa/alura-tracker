<template>
    <div class="box has-text-weigth-bold">
        <slot></slot>
    </div>
</template>

<script lang="ts">

import { defineComponent } from 'vue';

export default defineComponent({
    name: "BoxComun"
})

</script>


<style scoped>

    .box {
        background: var(--bg-task);
        color: var(--texto-task)
    }

</style>