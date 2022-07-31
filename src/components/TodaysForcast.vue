<template>
    <v-container>
        <h1 class="sectionTitle">Vandaag</h1>
          <slider ref="slider" class="slider" :options="options" style="margin-top: 1em;">
            <slideritem class="sliderCard" v-for="(item,index ) in todaysForcast" :key="item.id">
              <v-card class="Card forcastCard" >
                <v-card-title class="cardTitle forcastTitle" v-for="(time) in dayTime" :key="time.id">{{time[index]}}</v-card-title>
                <v-img alt="icon" :aspect-ratio="16/9" contain width="250px" class="img" v-bind:src="'../icons/'+item.weather[0].icon+'.svg'"></v-img>
                <v-card-text >
                  <p class="TodforcastTemp">{{Math.round(item.temp)}}°C</p>
                  <p class="TodforcastDesc">{{item.weather[0].description}}</p>
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
          pagination: true,
          currentPage: 0,
          slidesToScroll: 4,
          loop: false,
        },
        dayTime: [],
    };
  },
  created(){
    this.dayTime.push(this.weatherForcastTime)  
  }
};
</script>
<style>
  .slider-pagination{
    position: unset !important;
  }
</style>
<style scoped src="@/assets/css/style.css"></style>

