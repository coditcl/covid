<script context="module">
 import requests from "../data/requests.js";
 
 export async function preload(){
   try{
     
      const usStats = await requests.usStats();
      const historicUS = await requests.historicUS();
      const statesData = await requests.statesData();

      return {usStats, historicUS, statesData};
   } catch(e) {
     console.log(e);
     this.error(500, "There was an error in calling the api, pleasy try again in 5 minutes.");
     return;
   }
 }
</script>
<script>
import CovidStat from '../components/CovidStat.svelte';
import CovidChart from '../components/CovidChart.svelte';
import TableContainer from '../components/TableContainer.svelte';
export let usStats;
export let historicUS;
export let statesData;

console.log(historicUS, "historicUS");
console.log(usStats, "usStats");
console.log(statesData, "statesData");
</script>

<svelte:head>
<title>Covid 19 Tracker US</title>
</svelte:head>

<div class="section header">
  <div class="container">
   <h1>COVID 19 - US</h1>
  </div>
</div>

<CovidStat {...usStats}
 />

<CovidChart historicData={historicUS} title="US COVID 19" />

<TableContainer data={statesData} />