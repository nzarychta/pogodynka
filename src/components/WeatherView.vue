<template>
<div class="weatherView">
<h1>Weather</h1>



<div class="cityPicker">
    <input type="text" v-model='cityName'>
    <button @click="getLocation">Szukaj</button>
</div>


<div class="currentWeather">
    <h2>CURRENT WEATHER</h2>
    <WeatherSingle :current = "current"/>
</div>

<div class="dailyWeather">
   
    <h2>DAILY WEATHER</h2>

</div>
</div>
</template>

<script>
import WeatherSingle from'./WeatherSingle.vue'
export default {
    name:'WeatherView',
    components:{
      WeatherSingle: WeatherSingle
    },
    data(){
    return{
        cityName:"Gdańsk",
        lat:"",
        lon:"",
        current:{},
        daily:[],
        currentCity:"",
    

    }

},
methods:{
    getWeather(lat,lon){
      console.log("getWeather");
      fetch("https://api.openweathermap.org/data/2.5/onecall?lat="+lat+"&lon="+lon+"&exclude=minutely,hourly,alerts&appid=04d03c358e8933ac6823da54c340c97b")
      .then(dt=>dt.json())
      .then(dt =>{
      console.log(dt)
      this.dily = dt.daily;
      this.current = dt.current;
    })
    },
    getLocation(){
    
    fetch("http://api.openweathermap.org/geo/1.0/direct?q="+this.cityName+"&appid=04d03c358e8933ac6823da54c340c97b")
    .then(dt=> dt.json())

    .then(dt=>{
      this.cityName=dt[0].name;
      this.currentCity = dt[0].name;
      this.lat=dt[0].lat;
      this.lon=dt[0].lon;
      this.getWeather(dt[0].lat, dt[0].lon);  
    })

    }

},




created(){
    this.getLocation();
}
}
</script>

<style>

</style>