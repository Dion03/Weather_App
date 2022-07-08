<template>
    <v-container>
        <h1>Vandaag</h1>
          <slider ref="slider" :options="options" style="margin-top: 1em !important">
            <slideritem v-for="(item,index ) in todaysForcast" :key="item.id" style="width:23.5%; margin-right: 2% !important;">
              <v-card class="Card forcastCard" >
                <v-card-title class="cardTitle" v-for="(time) in dayTime" :key="time.id">{{time[index]}}</v-card-title>
                <v-img alt="icon" :aspect-ratio="16/9" contain width="250px" class="img" v-bind:src="'../icons/'+item.weather[0].icon+'.svg'"></v-img>
                <v-card-text >
                  <p><b style="font-size: 28px; margin-right: 1em !important">{{Math.round(item.temp)}}°C</b></p>
                  <p><b style="font-size: 20px; color: #7E7F7E !important; margin-right: 1.5em !important">{{item.weather[0].description}}</b></p>
                </v-card-text>
              </v-card>
            </slideritem>
          <div slot="loading">loading...</div>
      </slider>
    </v-container>
</template>
<script>
// import axios from 'axios';
// import moment from 'moment';
import { slider, slideritem } from 'vue-concise-slider'

export default {
  props:['todaysForcast', 'weatherForcastTime'],
  components:{slider, slideritem},
  name: "TodaysForcast",
  data() {
    return {
        options: {
          pagination: false,
          currentPage: 0,
          // infinite: 4,
          slidesToScroll: 4,
          loop: false
        },
        dayTime: [],

    };
  },
  created(){
    this.dayTime.push(this.weatherForcastTime)  
    console.log(this.dayTime)
  }
};
</script>
<style scoped src="@/assets/css/style.css"></style>

