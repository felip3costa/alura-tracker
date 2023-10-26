<template>
  <div class="box formulario">
    <div class="columns">
      <div
        class="column is-8"
        role="form"
        aria-label="Formulário para criação de uma nova tarefa"
      >
        <input
          type="text"
          class="input"
          placeholder="Qual tarefa você deseja iniciar?"
          v-model="descricao"
        />
      </div>
      <div class="column">
        <temporizador-tarefa @ao-temporizador-finalizado="finalizarTarefa" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import TemporizadorTarefa from "./Temporizador.vue";

export default defineComponent({
  name: "FormularioPlay",
  data() {
    return {
      descricao: "",
    };
  },
  emits: ["aoSalvarTarefa"],
  components: {
    TemporizadorTarefa,
  },
  methods: {
    finalizarTarefa(tempoDecorrido: number): void {
      this.$emit("aoSalvarTarefa", {
        duracaoEmSegundos: tempoDecorrido,
        descricao: this.descricao,
      });
      this.descricao = "";
    },
  },
});
</script>

<style scoped>
  .box {
    margin: 10px;
  }
</style>

<style>
  .formulario {
    background-color: var(--bg-secundario);
  }
</style>