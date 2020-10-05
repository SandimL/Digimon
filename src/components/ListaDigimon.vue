<template>
  <v-container>
        <v-card dark v-for="digimon in digimons" v-bind:key="digimon" class="ma-5">
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
        digimons: []
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
        }
    }
  }
</script>
