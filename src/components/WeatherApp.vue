<template>
  <v-container class="pa-0 white-text" fluid style="padding: 0 !important;">
       <v-row no-gutters height="100%" >
          <v-col cols="4" sm="12" md="3">
            <!-- Search bar -->
            <v-card color="#18212D" style="border-radius: 0px !important; height: 100vh;" >
              <v-card-title>           
                <v-text-field
                  dark
                  style="background-color : #222A39; border-radius: 1em !important;"
                  prepend-icon="mdi-magnify"
                  v-model="city"
                  v-on:key.enter="getWeather">
                </v-text-field>
              </v-card-title>
              <!--  Temp -->
              <v-card class="Card ">
                <v-img alt="icon" :aspect-ratio="16/9" contain max-width="700" v-bind:src="this.weatherIcon+'.svg'"></v-img>
                <v-card-title class="mt-10 cardTitle" style="font-size: 64px !important; margin-bottom: -1rem;">
                  {{this.temp}}
                </v-card-title><br/>
                <v-card-text style="margin-left: 1rem;" class="cardText">
                  Voelt aan als {{this.feels_like}} °C <br/><br/> {{this.weather.weather[0].description}}           
                </v-card-text>              
                <v-divider color="#3A435F"></v-divider>
                <v-card-actions>
                  <v-card-text  class="cardText" >
                    <p class="mt-16"><v-icon >mdi-map-marker</v-icon>{{this.city}}, {{this.weather.sys.country}}: Woensdag 23:59</p>
                  </v-card-text>
                </v-card-actions>
              </v-card>      
            </v-card>
          </v-col>
          <!-- 2nd col -->
          <v-col cols="12" sm="12" md="9">
            <v-container  style="background-color: #222B3A;height: 100vh" >
                <TodaysForcast :city="this.city"></TodaysForcast>
                <WeatherHighlights :weatherInfo="this.weather"></WeatherHighlights>



            </v-container>
          </v-col>
        </v-row>
  </v-container>
</template>
<script>
import WeatherHighlights from "./WeatherHighlights"
import TodaysForcast from "./TodaysForcast"

import axios from "axios";
  export default {
    components:{WeatherHighlights, TodaysForcast},
    name: 'WeatherApp',
    data: () => ({
      weather: '',
      temp: '',
      feels_like: '',
      weatherIcon: '',
      city: 'Zwolle',
     
      items: [

      ]
    }),
    methods:{
      getWeather() {
        axios.get('https://api.openweathermap.org/data/2.5/weather?q='+ this.city +'&units=metric&APPID=1482f10b395eba6d7f743494cbc50429').then(response => {
          this.weather = response.data;
          
          console.log("Data:",response.data)
          this.temp = Math.round(response.data.main.temp) + "°C";
          this.feels_like = Math.round(response.data.main.feels_like);
          this.weatherIcon = response.data.weather[0].icon;

          this.items.push(this.weather.clouds.all, this.weather.main.humidity ,this.weather.main.pressure ,Math.round(this.weather.wind.speed))

                    console.log(this.items)

        })
      },

    },
    mounted(){
      this.getWeather()
    }
  }
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
</style>

