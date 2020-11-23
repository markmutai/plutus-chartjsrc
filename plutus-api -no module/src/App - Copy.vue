<template>
  <div id="app" class="container">
    <div class="row mt-5">
      <div class="col">
        <h2>Positive</h2>
        <!-- <line-chart :chartData="arrPossitive" :options="charOptions" label="Positive"></line-chart> -->
      </div>

    </div>
  </div>
</template>

<script>
import axios from 'axios';
import moment from 'moment';

// import LineChart from './components/LineChart';

export default {
  name: "App",
  components: {},
  data(){
    return{
      arrNew:[],
      arrRecovered:[],
      arrDeaths:[]
      };
  },
  async created(){
    const { data } = await axios.get("https://api.covid19api.com/summary");
    // console.log(data);
    data.forEach(d=>{
     const date = moment(d.date, "YYYYMMDDHHmm").format("MM/DD");
     
     const{
       NewConfirmed,
       NewRecovered,
       NewDeaths
       } = d;

        this.arrNew.push({date, total:NewConfirmed});        
        this.arrRecovered.push({date, total:NewRecovered});
        this.arrDeaths.push({date, total:NewDeaths});
        // console.log(this.arrNew);
    });
  }
};
</script>

<style></style>
