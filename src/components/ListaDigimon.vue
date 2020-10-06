<template>
  <v-container>
        <v-card dark v-for="digimon in digimons" v-bind:key="digimon" class="ma-5"
         v-bind:style="{ backgroundColor: selecionaCor(digimon.level)}"
        >
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
  export default {
    name: 'ListaDigimon',

    data: () => ({
        digimons: [],
        teste: 'tesssttee',
        colorByLevels: {'In Training': '#E0AAFF', 'Training': '#C77DFF', 'Rookie': '#9D4EDD', 'Champion': '#7B2CBF', 'Ultimate': '#5A189A', 'Fresh': '#3C096C', 'Mega': '#240046', 'Armor': '#10002B'}
    }),
    mounted () {
        this.requisicaoDigimons();
    },
    methods:{
        requisicaoDigimons: function(){
            axios
            .get('https://digimon-api.herokuapp.com/api/digimon')
            .then(response => (
                this.digimons = response.data
            ))
            .catch(e => {
                console.error("Erro ao realizar requisição", e)
            })
        },
        selecionaCor: function(level){
            return this.colorByLevels[level]
        }
    }
  }
</script>
