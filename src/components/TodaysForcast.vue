<template>
    <v-container>
        <h1>Het weer van vandaag</h1>
              <v-row >
                <v-col v-for="item in todaysForcast" :key="item.id">
                  <v-card class="Card forcastCard" >
                    <v-card-title class="cardTitle">{{item.dt}}</v-card-title>
                    <v-img alt="icon" :aspect-ratio="16/9" contain v-bind:src="item.weather[0].icon+'.svg'"></v-img>
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
import axios from 'axios';
import moment from 'moment'
export default {
  props:['city'],
  name: "WeatherHighlights",
  data() {
    return {
        forcastWeather: '',
        todaysForcast: []
    };
  },
  methods:{
  getWeatherForcast() {
        axios.get('https://api.openweathermap.org/data/2.5/forecast?q='+ this.city +'&units=metric&APPID=1482f10b395eba6d7f743494cbc50429').then(response => {
          this.forcastWeather = response.data;
          console.log("Future weather",response.data);
          var weatherArray = Object.values(response.data.list);
          weatherArray.forEach(element => {
            if(moment().format('YYYY-MM-DD') == moment(element.dt_txt).format('YYYY-MM-DD')){
              this.todaysForcast.push(element);
              console.log("Weer nu",element);
            }
          });
        })
      },
  },
  mounted(){
    this.getWeatherForcast()
    console.log("Wordt mee gestuurd",this.weatherInfo)
    console.log("Weer vandaag",this.todaysForcast)
  },
  watch:{
    city(){
        this.todaysForcast = []
        this.getWeatherForcast()
    }
  }

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

</style>
