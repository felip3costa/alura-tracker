<template>
    <box-comun>
        <div class="columns">
            <div class="column is-7">
                {{ item.descricao || 'Tarefa sem descrição' }}
            </div>
            <div class="column">
                <cronometro-tarefa :tempoEmSegundos="item.duracaoEmSegundos"/>
            </div>
        </div>
    </box-comun>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import ITarefa from "../interfaces/ITarefa";
import CronometroTarefa from "./Cronometro.vue";
import BoxComun from "./Box.vue"

export default defineComponent({
  name: "TarefaLista",
  components: {
    CronometroTarefa,
    BoxComun,
  },
  props: {
    item: {
        type: Object as PropType<ITarefa>,
            required: true,
    }
  }
});

</script>