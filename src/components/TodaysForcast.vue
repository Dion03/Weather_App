<template>
    <v-container>
        <h1>Het weer van vandaag</h1>
              <v-row >
                <v-col v-for="(item) in todaysForcast" :key="item.id">
                  <v-card class="Card forcastCard" >
                    <v-card-title class="cardTitle">{{item.dt_txt.split(" ").slice(1)[0]}}</v-card-title>
                    <v-img alt="icon" :aspect-ratio="16/9" contain width="250px" class="img" v-bind:src="item.weather[0].icon+'.svg'"></v-img>
                    <v-card-text class="cardText">
                      <p>{{Math.round(item.main.temp)}}</p>
                      <p>{{item.weather[0].description}}</p>
                    </v-card-text>
                  </v-card>
                  
                </v-col>
              </v-row>
    </v-container>
</template>
<script>
// import axios from 'axios';

export default {
  props:['todaysForcast'],
  name: "WeatherHighlights",
  data() {
    return {

    };
  },
};
</script>
<style scoped>
* {
    font-family: "Roboto" !important; 
    color: white !important;
    margin: 0 !important;
  }
  .Card{
    justify-content: center !important;
    text-align: center !important;
    background-color: #18212D !important;
    border-radius: 2em !important;
  }
  .leftCard{
    border-radius: 0px !important 
  }
  .cardTitle{
    justify-content: center !important;
  }
  .cardText{
    font-size:large;
  }
  .img{
  left: 50%;
  transform: translate( -50%);
  }

</style>
