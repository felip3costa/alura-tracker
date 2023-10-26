<template>
  <main class="columns is-gapless is-multiline" :class="{'modo-escuro': modoEscuroAtivo}">
    <div class="column is-one-quarter">
      <barra-lateral @aoTemaAlterado="trocarTema"/>
    </div>
    <div class="column is-three-quarter conteudo">
      <formulario-play @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <tarefa-lista
          v-for="(tarefa, index) in tarefas"
          :key="index"
          :item="tarefa"
        />
        <box-comun v-if="listaEstaVazia">
          Você não iniciou nenhuma tarefa
        </box-comun>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import BarraLateral from "./components/BarraLateral.vue";
import FormularioPlay from "./components/Formulario.vue";
import TarefaLista from "./components/Tarefa.vue";
import BoxComun from "./components/Box.vue";
import ITarefa from "./interfaces/ITarefa";

export default defineComponent({
  name: "App",
  data() {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false,
    };
  },
  computed: {
    listaEstaVazia(): boolean {
      return this.tarefas.length === 0;
    },
  },
  methods: {
    salvarTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa);
    },
    trocarTema(modoEscuroAtivo: boolean) {
      if (modoEscuroAtivo) {
        this.modoEscuroAtivo = true;
      } else {
        this.modoEscuroAtivo = false;
      }

    }
  },
  components: {
    BarraLateral,
    FormularioPlay,
    TarefaLista,
    BoxComun,
  },
});
</script>

<style scoped>
.lista {
  padding: 10px;
}
main {
  --bg-navbar: #dfdfdf;
  --bg-primario: #fff;
  --bg-secundario: #ededed;
  --texto-primario: #000;
  --bg-task: #daffd7;
  --texto-task: #050101;
}

main.modo-escuro {
  --bg-navbar: #1b1b24;
  --bg-primario: #2b2d42;
  --bg-secundario: #474967;
  --texto-primario: #ddd;
  --bg-task: #41b883;
  --texto-task: #f7f7f7;
}

.conteudo {
  background-color: var(--bg-primario);
}
</style>
