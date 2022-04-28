<template>
  
      <table BORDER="1">
    <tr>
        <th>DATE</th>
        <td>{{current.dt}}</td>
    </tr> 
      <tr>
        <th>TEMP</th>
        <td>{{current.temp}}</td>
    </tr>
        <tr>
        <th>DESC</th>
        <td>{{current.weather?.[0].description}}</td>

        
    </tr> 
      <tr>
          <th>ICON</th>
          
          <img 
          v-if="current.weather?.[0].icon"
          :src ="'http://openweathermap.org/img/wn/'+current.weather?.[0].icon+'@2x.png'" alt="Ikona"> 
          
          
        </tr>
</table>
  
</template>

<script>
export default {
    props:{
        current: Object
    }

}
</script>

<style>

</style>