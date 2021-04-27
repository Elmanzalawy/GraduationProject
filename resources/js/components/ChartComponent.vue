<template>
  <div>
    <!-- <button v-on:click="modifyData()">Click</button> -->
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
        labels: [],
        datasets: [{
            label: 'Sensor Reading',
            data: [],
              backgroundColor: "rgba(71, 183,132,.5)",
              borderColor: "#47b784",
              borderWidth: 3
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
      this.getReadings()
  },
    methods: {
        getReadings() {
            console.log('fetch')
            axios.get('/api/readings').then(response => {
                response.data.forEach(reading => {
                    this.sensorData.labels.push(reading.created_at)
                    this.sensorData.datasets[0].data.push(reading.value)
                });

                this.componentKey++;
                console.log(this.sensorData)
            });
        }
    }
}
</script>
