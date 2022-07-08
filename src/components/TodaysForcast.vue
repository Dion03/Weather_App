<template>
    <v-container>
        <h1>Het weer van vandaag</h1>
              <!-- <v-row >
                <v-col> -->
                  
                     <slider ref="slider" :options="options">
          <!-- slideritem wrapped package with the components you need -->
          <slideritem v-for="(item, index) in todaysForcast" :key="item.id" style="width:23.5%; margin-right: 2% !important;"><v-card class="Card forcastCard" >
                    <v-card-title class="cardTitle"><!--{{item.dt.split(" ").slice(1)[0]}} -->{{12 + index + ":00"}}</v-card-title>
                    <v-img alt="icon" :aspect-ratio="16/9" contain width="250px" class="img" v-bind:src="item.weather[0].icon+'.svg'"></v-img>
                    <v-card-text class="cardText">
                      <p>{{Math.round(item.temp)}} °C</p>
                      <p>{{item.weather[0].description}}</p>
                    </v-card-text>
                  </v-card></slideritem>
          <!-- Customizable loading -->
          <div slot="loading">loading...</div>
      </slider>
                <!-- </v-col>
              </v-row> -->
    </v-container>
</template>
<script>
// import axios from 'axios';
// import moment from 'moment';
import { slider, slideritem } from 'vue-concise-slider'

export default {
  props:['todaysForcast'],
  components:{slider, slideritem},
  name: "WeatherHighlights",
  data() {
    return {
        options: {
              pagination: false,
           currentPage: 0,
  infinite: 4,
  slidesToScroll: 4,
  loop: false
        },
        style: {
  'background': '#7caabe',
  'width': '23.5%',
  'margin-right': '2%'
}
    };
  },
  mounted(){
    console.log("ashjjvhjjjh",this.todaysForcast)
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
  .img{
  left: 50%;
  transform: translate( -50%);
  }

</style>
