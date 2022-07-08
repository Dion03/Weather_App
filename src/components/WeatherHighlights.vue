<template>
<v-container>
  <h1>Weerstatestieken van vandaag</h1>
   <v-row>
        <v-col md="3">
            <v-card class="Card forcastCard" >
                <v-card-title class="cardTitle">Luchtvochtigheid</v-card-title>
                <v-img alt="icon" :aspect-ratio="16/9" contain max-width="200" class="img"  v-bind:src="'humidity.svg'"></v-img>
                <v-card-text class="cardText">{{this.weatherInfo.main.humidity}}% </v-card-text>
            </v-card>
        </v-col>
        <v-col md="3">
            <v-card class="Card forcastCard" >
                <v-card-title class="cardTitle">Bewolking</v-card-title>
                <v-img alt="icon" :aspect-ratio="16/9" contain max-width="200" class="img" v-bind:src="'clouds.svg'"></v-img>
                <v-card-text class="cardText">{{this.weatherInfo.clouds.all}}%</v-card-text>
            </v-card>
        </v-col>
        <v-col md="3">
            <v-card class="Card forcastCard" >
                <v-card-title class="cardTitle">Windkracht/snelheid</v-card-title>
                <v-img alt="icon" :aspect-ratio="16/9" contain max-width="200" class="img" v-bind:src="'wind.svg'"></v-img>
                <v-card-text class="cardText">{{Math.round(this.weatherInfo.wind.speed)}} Km/h</v-card-text>
            </v-card>
        </v-col>
        <v-col md="3">
            <v-card class="Card forcastCard" >
                <v-card-title class="cardTitle">Luchdruk</v-card-title>
                <v-img alt="icon" :aspect-ratio="16/9" contain max-width="200" class="img" v-bind:src="'pressure.svg'"></v-img>
                <v-card-text class="cardText">{{this.weatherInfo.main.pressure}}hPa</v-card-text>
            </v-card>
        </v-col>
    </v-row>
</v-container>
   
</template>
<script>
export default {
  props:['weatherInfo'],
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
