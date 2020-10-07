<template>
  <v-container>
        <v-img
          :src="require('../assets/logo.png')"
          class="my-3"
          contain
          height="200"
        />
        <div>
            <v-text-field type="text" class="ma-15" label="Buscar Digimon por nome" v-model="busca" /> 
        </div>
        <v-row v-show="carregando" style="justify-content: center" class="ma-15">
            <breeding-rhombus-spinner
            :animation-duration="1000"
            :size="80"
            color="#3C096C"/>
        </v-row>
        <v-card dark v-for="digimon in DigimonsFiltrados" v-bind:key="digimon" class="ma-5"
         v-bind:style="{ backgroundColor: selecionaCor(digimon.level)}">
            <div class="d-flex flex-no-wrap justify-space-between" >
                <div>
                    <v-card-title class="headline" v-text="digimon.name">
                    </v-card-title>
                    <v-card-subtitle v-text="digimon.level"></v-card-subtitle>
                </div>
                <v-avatar class="ma-3" size="125" item>
                    <v-img :src="digimon.img"></v-img>
                </v-avatar>
            </div>
        </v-card>
  </v-container>
</template>

<script>
import axios from 'axios'
import {BreedingRhombusSpinner} from 'epic-spinners'

  export default {
    name: 'ListaDigimon',
    components: {
      BreedingRhombusSpinner
    },
    data: () => ({
        busca: '',
        carregando: true,
        digimons: [],
        colorByLevels: {'In Training': '#E0AAFF', 'Training': '#C77DFF', 'Rookie': '#9D4EDD', 'Champion': '#7B2CBF', 'Ultimate': '#5A189A', 'Fresh': '#3C096C', 'Mega': '#240046', 'Armor': '#10002B'}
    }),
    mounted () {
        this.requisicaoDigimons();
    },
    methods:{
        requisicaoDigimons: function(){
            axios
            .get('https://digimon-api.herokuapp.com/api/digimon')
            .then(response => {
                this.digimons = response.data
                this.carregando = false
            })
            .catch(e => {
                console.error("Erro ao realizar requisição", e)
                this.carregando = false
            })
        },
        selecionaCor: function(level){
            return this.colorByLevels[level]
        }
    },
    computed: {
        DigimonsFiltrados() {
            this.carregando = true
            return this.digimons.filter(digimon => {
                this.carregando = false
                return digimon.name.toLowerCase().includes(this.busca.toLowerCase())
            })
        }
    }
  }
</script>
