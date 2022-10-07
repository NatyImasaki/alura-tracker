<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <Cronometro :tempoEmSegundos="tempoEmSegundos" />
        <Botao @clicado="iniciar" :desabilitado="cronometroParado" icone="fas fa-play" texto="play"/>
        <Botao @clicado="finalizar" :desabilitado="!cronometroParado" icone="fas fa-stop" texto="stop"/>
    </div>               
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Cronometro from './Cronometro.vue'
import Botao from './Botao.vue'

export default defineComponent({
    name: 'Temporizador',

    emits: ['aoTemporizadorFinalizado'],

    components: {
        Cronometro,
        Botao
    },

    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroParado: false
        }
    },

    methods: {
        iniciar(){
            this.cronometroParado = true
            this.cronometro = setInterval(() => {
                this.tempoEmSegundos += 1
            }, 1000)
        },

        finalizar(){
            this.cronometroParado = false
            clearInterval(this.cronometro)
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            this.tempoEmSegundos = 0
        }
    }
})
</script>