<template>
  <div>
    <button v-on:click="modifyData()">Click</button>
    <line-chart v-model="sensorData" v-bind:chartdata="sensorData" v-bind:options="options" :key="componentKey"/>
  </div>
</template>

<script>
// import { Line} from 'vue-chartjs';
// import {Chart} from 'chart.js'
import LineChart from './Chart.vue'

export default {
  name: 'LineChartContainer',
components: { LineChart },

  data(){
    return {
        componentKey: 0,
      sensorData: {
        labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
        datasets: [{
            label: 'Sensor Reading',
            data: [12, 19, 53, 25, 32, 43],
            backgroundColor: [
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)'
            ],
            borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)'
            ],
            borderWidth: 1
        }]
      },
        options: {
            responsive: true,
            maintainAspectRatio: false
        }
    }
  },

  mounted() {
      console.log('mounted')
  },
  methods:{
      modifyData(){
        console.log(this.sensorData.datasets[0].data[0])
        this.sensorData.datasets[0].data[0] = 44;
        this.componentKey += 1;
      }
  }
}
</script>
