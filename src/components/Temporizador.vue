<template>
  <div class="is-flex is-align-items-center is-justify-content-space-between">
    <cronometro-tarefa :tempoEmSegundos="tempoEmSegundos" />

    <button class="button" @click="iniciar" :disabled="canPlay">
      <span class="icon">
        <i class="fas fa-play"></i>
      </span>
    </button>
    <button class="button" @click="finalizar" :disabled="canStop">
      <span class="icon">
        <i class="fas fa-stop"></i>
      </span>
    </button>
  </div>
</template>


<script lang="ts">
import { defineComponent } from "vue";
import CronometroTarefa from "./Cronometro.vue";

export default defineComponent({
  name: "TemporizadorTarefa",
  emits: ["aoTemporizadorFinalizado"],
  data() {
    return {
      tempoEmSegundos: 0,
      cronometro: 0,
      cronometroRodando: false,
      canPlay: false,
      canStop: true,

    };
  },
  components: {
    CronometroTarefa,
  },
  methods: {
    clicou() {
      this.canPlay = !this.canPlay
      if (!this.canStop) {
        this.canStop = !this.canStop
      } else {
        let timeToStop = setInterval(() => {
          this.canStop = !this.canStop
          clearInterval(timeToStop)
        }, 5000)
        
      }
      
    },
    iniciar() {
      this.cronometro = setInterval(() => {
        this.tempoEmSegundos += 1;
      }, 1000);

      this.clicou()

    },
    finalizar() {
      this.clicou()
      clearInterval(this.cronometro);
      this.$emit("aoTemporizadorFinalizado", this.tempoEmSegundos);
      this.tempoEmSegundos = 0;
    },
  },
});
</script>