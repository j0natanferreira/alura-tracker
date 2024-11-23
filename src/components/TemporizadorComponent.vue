<template>
    <section class="is-flex is-align-items-center is-justify-content-space-between">
        <CronometroComponent :tempoEmSegundos="tempoEmSegundos"/>
        <BotaoComponent 
            @clicado="iniciar" 
            icone="fas fa-play" 
            texto="play" 
            :desabilitado="cronometroRodando"
        />
        <BotaoComponent 
            @clicado="finalizar" 
            icone="fas fa-stop" 
            texto="stop" 
            :desabilitado="!cronometroRodando"
        />
    </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import BotaoComponent from './BotaoComponent.vue';
import CronometroComponent from './CronometroComponent.vue'

export default defineComponent({
    name: 'TemporizadorComponent',
    emits: ['aoTemporizadorFinalizado'],
    components: { 
        CronometroComponent,
        BotaoComponent 
    },
    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false
        }
    },
    methods: {
        iniciar() {
            // Comerçar a contagem
            this.cronometroRodando = true;
            this.cronometro = setInterval(()=> {
                this.tempoEmSegundos += 1
            }, 1000);
        },
        finalizar() {
            this.cronometroRodando = false;
            clearInterval( this.cronometro );
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos);
            this.tempoEmSegundos = 0;
        }
    }
})
</script>

<style scoped>

</style>