<template>
  <div>
      <v-container>
          <v-layout :wrap="true">
            <v-flex xs12>
                <v-card>
                    <v-date-picker
                    v-model="date"
                    full-width
                    :min="min"
                    :max="max"
                    @change="getDolar(date)"
                    color="success"
                    >

                    </v-date-picker>
                </v-card>
                <v-card color="info"
                    dark>
                        <v-card-text class="display-1 text-center">
                        Dolar price:  {{value}}
                        </v-card-text>
                </v-card>
            </v-flex>
         </v-layout>
      </v-container>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data(){
    return {
        date: new Date().toISOString().substr(0, 10),
        min: "1984",
        max: new Date().toISOString().substr(0, 10),
        value: null
    }
  },
  methods: {
      async getDolar(day){
          let arrayDate = day.split(["-"])
          let ddmmyy = arrayDate[2]+"-"+arrayDate[1]+"-"+arrayDate[0]

          try {
            let data = await axios.get(`https://mindicador.cl/api/dolar/${ddmmyy}`)
            if(data.data.serie.length > 0) {
                this.value = await data.data.serie[0].valor
            } else {
                this.value = "unavailable"
            }
          } catch(err) {
            // eslint-disable-next-line no-console
            console.log(err)
          }
      }
  },
  created () {
    this.getDolar(this.date);
  }
};
</script>
