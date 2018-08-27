<template>
  <div id="app">
    <Navigation/><br><br>
    <img alt="Vue logo" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRcottslsjrIhX2eyAz4h_4k1oixBC1oocAK_LjHDno_aRToYl3"><br><br><br>
    <v-text-field
              v-model="city"
              box
              label="CITY:COUNTRYCODE"
              clearable
            ></v-text-field>
      <v-btn class="button-format" v-on:click = "display()" small>Search Weather</v-btn>
      <v-btn class="button-format" v-on:click = "clearR()" small>Clear Result</v-btn><br><br><br>
      <div v-if="!seen" class="result">
        <h2>Search Result:</h2><br>
        <ul style="list-style-type:none">
           <li v-for="item in weatherInfo">
              <div v-for="(value,key) in item">
                 <strong>{{key}}</strong> {{value}}
              </div>
           </li>
        </ul>
      </div><br><br><br><br><br><br><br><br><br>
      <Footer/>
  </div>
</template>

<script type="text/javascript">
import Navigation from './components/Navigation.vue';
import Footer from './components/Footer.vue';
import axios from 'axios';

      export default{
            name: 'app',
            components: {
              Navigation,
              Footer
            },
            data(){
              return{
                 seen:true,
                 city:'',
                 weatherInfo:[
                   {
                    Coordinate:'',
                    Weather:'',
                    Base:'',
                    MainData:'',
                    Visibility:'',
                    Wind:'',
                    Cloud:'',
                    Dt:'',
                    Sun:'',
                    ID_Name_Code:'',
                    HTTP_Request_Status:'',
                    HTTP_Header:'',
                    HTTP_Config:'',
                    HTTP_Request:''
                   }
                 ]
              }
            },

            methods : {
               clearR(){
                this.seen = true;
               },             
               display(){
                  this.seen = false;
                  axios
                      .get('http://api.openweathermap.org/data/2.5/weather?q='+this.city+'&APPID=36f52178bc34b295cd30a8739bc93d8c')
                      .then(response => (
                        this.weatherInfo[0].Coordinate = response.data.coord,
                        this.weatherInfo[0].Weather = response.data.weather,
                        this.weatherInfo[0].Base = response.data.base,
                        this.weatherInfo[0].MainData = response.data.main,
                        this.weatherInfo[0].Visibility = response.data.visibility,
                        this.weatherInfo[0].Wind = response.data.wind,
                        this.weatherInfo[0].Cloud = response.data.clouds,
                        this.weatherInfo[0].Dt= response.data.dt,
                        this.weatherInfo[0].Sun= response.data.sys,
                        this.weatherInfo[0].ID_Name_Code= response.data.id+"-"+response.data.name+"-"+response.data.cod,
                        this.weatherInfo[0].HTTP_Request_Status= response.status+"-"+response.statusText,
                        this.weatherInfo[0].HTTP_Header= response.headers,
                        this.weatherInfo[0].HTTP_Config= response.config,
                        this.weatherInfo[0].HTTP_Request= response.request
                      ))
                  this.city="";
               }
            }
       }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e5i;
  margin-top: 6ipx;
}

.button-format{
  text-transform: none !important;
  width:120px !important;
}

.result{
  background-color: lightgrey;
  border: 2px solid black;
  text-align:left;
}
</style>
