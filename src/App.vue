<template>
  <div id="app" class="container">
    <div class="row mt-5">
      <div class="col">
        <!-- <p>{{arrVolume}}</p> -->
        <div class="row mt-5" v-if="arrVolume.length > 0">
            <div class="col">
              <h2 class="text-center">Px Volume - Plutus API</h2>
              <line-chart
              :chartData="arrVolume"
              :options="chartOptions"
              :chartColors="positiveChartColors"
              label="pxVolume"
              />
            </div>
        </div>
        <div class="row mt-5" v-if="arrClose.length > 0">
          <div class="col">
            <h2 class="text-center">Px Close - Plutus API</h2>
            <line-chart
            :chartData="arrClose"
            :options="chartOptions"
            :chartColors="closeChartColors"
            label="pxClose"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import moment from 'moment';
import '../node_modules/bootstrap/dist/css/bootstrap.min.css';

import LineChart from './components/LineChart';

export default {
  name: "App",
  components: {
    LineChart
  },
  data(){
    return{
      arrVolume: [],
      positiveChartColors: {
        borderColor: "#077187",
        pointBorderColor: "#0E1428",
        pointBackgroundColor: "#AFD6AC",
        backgroundColor: "#74A57F"
      },
      arrClose: [],
      closeChartColors: {
        borderColor: "#251F47",
        pointBorderColor: "#260F26",
        pointBackgroundColor: "#858EAB",
        backgroundColor: "#858EAB"
      },
      };
  },
  async created(){
    const { data } = await axios.get("https://api-devops.azure-api.net/v1/plutus/data/all");

    console.log(data);
    // console.log(totals);

    data.responseObject.forEach(d=>{
    const date = moment(d.tradingDate, "YYYYMMDDHHmm").format("DD/MM/YY");
    // console.log(date);
    // const totals = (d.pxClose);

    // console.log(totals);

    const{      
      pxVolume,
      pxClose
    } = d;

    this.arrVolume.push({date, total: pxVolume});
    this.arrClose.push({date, total: pxClose});    
     
    });
  }
};
</script>

<style></style>