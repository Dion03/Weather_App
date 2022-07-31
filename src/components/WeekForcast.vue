<template>
<v-container>
  <h1 class="sectionTitle">Weer in het verloop van de week</h1>
    <v-row >
        <v-col md="3" cols="6" v-for="(item, index) in weekForcast" :key="item.id">
            <v-card height="100%" class="Card forcastCard" >
                <v-card-title class="cardTitle test3"  v-for="(time) in dayTime" :key="time.id">{{time[index]}}</v-card-title>
                <v-img alt="icon" :aspect-ratio="16/9" contain width="250px" class="img" v-bind:src="'../icons/'+item.weather[0].icon+'.svg'"></v-img>
                <v-card-text class="cardTitle">
                    <span class="dailyTempText">{{Math.round(item.temp.max)}}°C</span> 
                    <span class="dailyTempSubText">{{Math.round(item.temp.min)}}°C</span>
                    <p class="WeekforcastDesc">{{item.weather[0].description}}</p>
                </v-card-text>
            </v-card>
        </v-col>
    </v-row>
</v-container>
</template>
<script>
export default {
  props:['weekForcast', 'weeklyWeatherForcastTime'],
  name: "WeekForcast",
  data() {
    return {
        dayTime: []
    };
  },
  created(){
    this.dayTime.push(this.weeklyWeatherForcastTime )  
  }
};
</script>

<style scoped src="@/assets/css/style.css"></style>
