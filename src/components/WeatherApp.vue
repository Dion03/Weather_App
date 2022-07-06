<template>
  <v-container class="fill-height white--text" fluid>
       <v-row no-gutters height="100%">
          <v-col cols="4" sm="12" md="3" height="100%">
            <!-- Search bar -->
            <v-card color="#18212D" style="border-radius: 0px !important" >
              <v-card-title>           
                  <v-text-field
                    style="background-color: #222A39; color: darkgray !important;"
                    hide-details
                    prepend-icon="mdi-magnify"
                    single-line
                    v-model="city"
                    v-on:keyup.enter="getWeather"
                    >
                  </v-text-field>
                </v-card-title>
            </v-card>
            
            <!--  Temp -->
            <v-card color="#18212D" style="min-height: 85vh;border-radius: 0px !important ">
              <v-img alt="icon" :aspect-ratio="16/9" contain max-width="500" v-bind:src="this.weatherIcon+'.svg'"></v-img>
              <v-card-title class="text mt-10" style="font-size: 64px !important; margin-bottom: -1rem;">
                {{this.temp}}
              </v-card-title><br/>
              <v-card-text style="font-size: 18px !important; margin-left: 1rem;" class="text">
                Feels like {{this.feels_like}} °C <br/><br/> {{this.weather.weather[0].description}}           
              </v-card-text>              
              <v-divider color="#3A435F"></v-divider>
              <v-card-actions>
                <v-card-text class="text" >
                  <p class="mt-16"><v-icon >mdi-map-marker</v-icon>{{this.city}}, Woensdag 23:59</p>
                </v-card-text>
                <p  style="font-size: 18px !important" ></p> 
                <p> </p>
              </v-card-actions>
            </v-card>          
          </v-col>

          <!-- 2nd col -->
          <v-col cols="12" sm="12" md="9">
            <v-container color="#222B3A" style="min-height: 94.6vh; background-color: #222B3A;">
            </v-container>
          </v-col>
        </v-row>
  </v-container>
</template>
<script>
import axios from "axios";
  export default {
    name: 'WeatherApp',
    data: () => ({
      weather: '',
      temp: '',
      feels_like: '',
      weatherIcon: '',
      city: 'Zwolle'
    }),
    methods:{
      getWeather() {
        console.log("getWeather");
        axios.get('https://api.openweathermap.org/data/2.5/weather?q='+ this.city +'&units=metric&APPID=1482f10b395eba6d7f743494cbc50429').then(response => {
          this.weather = response.data;
          console.log(response.data)
          this.temp = Math.round(response.data.main.temp) + "°C";
          this.feels_like = Math.round(response.data.main.feels_like);
          this.weatherIcon = response.data.weather[0].icon;
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
</style>

