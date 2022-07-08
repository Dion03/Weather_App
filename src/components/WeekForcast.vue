<template>
<v-container>
  <h1>Weer rest van de week</h1>
              <v-row >
                <v-col md="3" v-for="(item) in weekForcast" :key="item.id">
                  <v-card class="Card forcastCard" >
                    <v-card-title class="cardTitle">Zaterdag</v-card-title>
                                    <v-img alt="icon" :aspect-ratio="16/9" contain width="250px" class="img" v-bind:src="'../icons/'+item.weather[0].icon+'.svg'"></v-img>

                    <v-card-text class="cardTitle"><span class="dailyTempText">{{Math.round(item.temp.max)}}°C</span>    <span class="dailyTempSubText">{{Math.round(item.temp.min)}}°C</span></v-card-text>

                  </v-card>
                  
                </v-col>
              </v-row>
</v-container>
   
</template>
<script>
export default {
  props:['weekForcast'],
  name: "WeekForcast",
  data() {
    return {
    };
  },
  mounted(){
    console.log("Week forcast: ",this.weekForcast)
  }
};
</script>
<style scoped src="@/assets/css/style.css"></style>
