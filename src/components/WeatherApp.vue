<template>
  <v-container class="pa-0 white-text" fluid style="padding: 0; ">
       <v-row no-gutters height="100%" >
          <v-col cols="12" sm="12" md="3">
            <!-- Search bar -->
            <v-card color="#18212D" class="mainLeftCard">
              <v-card-title>           
                <v-text-field
                  dark
                  class="searchBar"
                  prepend-icon="mdi-magnify"
                  v-model="city"
                  v-on:keyup.enter="getWeather">
                </v-text-field>
              </v-card-title>
              <v-progress-circular
                indeterminate
                v-if="loading"
                :size="250">
              </v-progress-circular>
              <!--  Temp -->
              <v-card class="Card" v-if="!loading">
                <v-img alt="icon" :aspect-ratio="16/9" contain max-width="700" v-bind:src="'../icons/'+this.weatherIcon+'.svg'"></v-img>
                <v-card-title class="mt-10 cardTitle" style="font-size: 64px;">
                  {{this.temp}}
                </v-card-title><br/>
                <v-card-text class="cardText">
                  Voelt aan als {{this.feels_like}} °C <br/><br/> {{this.weather.weather[0].description}}           
                </v-card-text>              
                <v-divider color="#3A435F"></v-divider>
                <v-card-actions>
                  <v-card-text  class="cardText" >
                  <p class="mt-16"><v-icon >mdi-map-marker</v-icon>{{this.city}} {{this.weather.sys.country}},  {{this.time}}</p>
                  </v-card-text>
                </v-card-actions>
              </v-card>      
            </v-card>
          </v-col>
          <!-- 2nd col -->
          <v-col cols="12" sm="12" md="9">
            <v-container :class="loading ? 'loadingStyle' : 'normalStyle'" >
              <v-progress-circular
                class="mx-auto"
                indeterminate
                v-if="loading"
                :size="250">
              </v-progress-circular>
                <TodaysForcast v-if="!loading" :todaysForcast="this.todaysForcast" :weatherForcastTime="this.weatherForcastTime"></TodaysForcast>
                <WeatherHighlights v-if="!loading" :weatherInfo="this.weather"></WeatherHighlights>
                <WeekForcast v-if="!loading" :weekForcast="this.forcastWeather" :weeklyWeatherForcastTime="this.weeklyWeatherForcastTime"></WeekForcast>
            </v-container>
          </v-col>
        </v-row>
  </v-container>
</template>
<script>
import WeatherHighlights from "./WeatherHighlights"
import TodaysForcast from "./TodaysForcast"
import WeekForcast from "./WeekForcast"

import moment from 'moment'
import axios from "axios";
  export default {
    components:{WeatherHighlights, TodaysForcast, WeekForcast},
    name: 'WeatherApp',
    data: () => ({
      weather: '',
      temp: '',
      feels_like: '',
      weatherIcon: '',
      city: 'Zwolle',
      forcastWeather: [],
      todaysForcast: [],
      weatherForcastTime: [],
      weeklyWeatherForcastTime: [],
      time: '',
      loading: true
    }),
    methods:{      
      getGeoLocation(){
        if (navigator.geolocation) {
          navigator.geolocation.getCurrentPosition(this.getWeather)
        } 
      },
      getWeather() {
        setInterval(() => {}, 5000);
        axios.get('https://api.openweathermap.org/data/2.5/weather?q='+ this.city +'&units=metric&lang=nl&APPID='+process.env.VUE_APP_API_KEY).then(response => {
          this.weather = response.data;
          this.temp = Math.round(response.data.main.temp) + "°C";
          this.feels_like = Math.round(response.data.main.feels_like);
          this.weatherIcon = response.data.weather[0].icon;
        })
        .finally(() => {
          this.todaysForcast = [],
          this.forcastWeather = []
          this.getWeeklyForcast(this.weather.coord)
        })
      },
      getWeeklyForcast(coords){
        axios.get('https://api.openweathermap.org/data/2.5/onecall?lat=' + coords.lat + '&lon=' + coords.lon + '&exclude=minutely&units=metric&lang=nl&appid='+process.env.VUE_APP_API_KEY).then(response => {
          var weatherHourlyArray = Object.values(response.data.hourly);
          weatherHourlyArray.forEach(element => {
            this.todaysForcast.push(element);
            this.weatherForcastTime.push(moment.unix(element.dt).format('dddd, HH:mm'))
          })
          var weatherDailyArray = Object.values(response.data.daily);
          weatherDailyArray.forEach(element => {
            this.forcastWeather.push(element);
            this.weeklyWeatherForcastTime.push(moment.unix(element.dt).format('dddd'))
          })
          this.loading = false
        })
      },
      getTime(){
        this.time = moment().format("dddd HH:mm");
      },
    },
    mounted(){
      this.getWeather()
    },
    created() {
      this.time = moment().format("ddd, HH:mm");
      setInterval(() => this.getTime(), 1 * 1000);
    }
  }
</script>
<style scoped src="@/assets/css/style.css"></style>


