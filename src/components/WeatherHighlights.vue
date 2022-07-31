<template>
<v-container>
  <h1 class="sectionTitle">Weer statestieken</h1>
   <v-row>
        <v-col md="3" cols="6">
            <v-card height="100%" class="Card" >
                <v-card-title class="cardTitle">Luchtvochtigheid</v-card-title>
                <v-img alt="icon" :aspect-ratio="16/9" contain max-width="200" class="img" v-bind:src="'humidity.svg'"></v-img>
                <v-card-text class="cardText"><b class="highlightMainText">{{this.weatherInfo.main.humidity}}</b><b class="highlightSubText">%</b></v-card-text>
            </v-card>
        </v-col>
        <v-col md="3" cols="6">
            <v-card height="100%" class="Card" >
                <v-card-title class="cardTitle">Bewolking</v-card-title>
                <v-img alt="icon" :aspect-ratio="16/9" contain max-width="200" class="img" v-bind:src="'clouds.svg'"></v-img>
                <v-card-text class="cardText"><b class="highlightMainText">{{this.weatherInfo.clouds.all}}</b><b class="highlightSubText">%</b></v-card-text>
            </v-card>
        </v-col>
        <v-col md="3" cols="6">
            <v-card height="100%" class="Card" >
                <v-card-title class="cardTitle">Wind snelheid</v-card-title>
                <v-img alt="icon" :aspect-ratio="16/9" contain max-width="200" class="img" v-bind:src="'wind.svg'"></v-img>
                <v-card-text class="cardText"><b class="highlightMainText">{{ Number(this.weatherInfo.wind.speed*3.6).toFixed(1)}}</b><b class="highlightSubText"> km/u</b></v-card-text>
            </v-card>
        </v-col>
        <v-col md="3" cols="6">
            <v-card height="100%" class="Card" >
                <v-card-title class="cardTitle">Luchdruk</v-card-title>
                <v-img alt="icon" :aspect-ratio="16/9" contain max-width="200" class="img" v-bind:src="'pressure.svg'"></v-img>
                <v-card-text class="cardText"><b class="highlightMainText">{{this.weatherInfo.main.pressure}}</b><b class="highlightSubText"> hPa</b></v-card-text>
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
<style scoped src="@/assets/css/style.css"></style>
