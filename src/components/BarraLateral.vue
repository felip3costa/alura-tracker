<template>
  <header>
    <h1>
      <img src="../assets/logo.png"/>
    </h1>
    <a @click="alterarTema"><i :class="modoEscuroAtivo ? 'fa-solid fa-sun' : 'fa-solid fa-moon'"></i></a>
  </header>
</template>
<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "BarraLateral",
  emits: ["aoTemaAlterado"],
  data() {
    return {
      modoEscuroAtivo: false,
    };
  },
  computed: {
    textoBotao() {
      if (this.modoEscuroAtivo) {
        return "Desativar modo escuto";
      } else {
        return "Ativar modo escuto";
      }
    },
  },
  methods: {
    alterarTema() {
      this.modoEscuroAtivo = !this.modoEscuroAtivo;
      this.$emit("aoTemaAlterado", this.modoEscuroAtivo);
    },
  },
});
</script>

<style scoped>
header {
  background: var(--bg-navbar);
  width: 100%;
  height: 100vh;
  text-align: center;
}
h1 {
  text-align: center;
}
@media only screen and (max-width: 768px) {
  header {
    padding: 2.5rem;
    height: auto;
  }
}
</style>