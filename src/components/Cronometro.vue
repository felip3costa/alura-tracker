<template>
  <section>
    <strong class="cronometro">
      {{ tempoDecorrido }}
    </strong>
  </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "CronometroTarefa",
  props: {
    tempoEmSegundos: {
        type: Number,
        default: 0
    }
  },
  computed: {
    tempoDecorrido(): string {
      const tempo = new Date(this.tempoEmSegundos * 1000);
      return tempo.toISOString().substring(11, 19);
    },
  },
});
</script>

<style>
  .cronometro {
    color: var(--texto-primario);
  }
</style>