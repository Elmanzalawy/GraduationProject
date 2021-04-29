<template>
  <div>
    <line-chart v-model="sensorData" v-bind:chartdata="sensorData" v-bind:options="options" :key="componentKey"/>
  </div>
</template>

<script>
import LineChart from './Chart.vue'

export default {
  name: 'LineChartContainer',
components: { LineChart },

  data(){
    return {
      componentKey: 0,
      max_number_of_readings: 10,
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
        maintainAspectRatio: false,
        animation: false,
        scales: {
          yAxes: [
            {
              ticks: {
                beginAtZero: true,
                padding: 25
              }
            }
          ]
        }
      }
    }
  },

  mounted() {
      console.log('mounted')
      this.getReadings()

      Echo.private('sensor-reading')
        .listen('ReadingSent', (e) => {
            this.sensorData.labels.push(e.reading.created_at)
            this.sensorData.datasets[0].data.push(e.reading.value)

            // if number of readings exceeds n, filter out older readings
            this.updateReadingsArray();
            this.componentKey++;
        });
  },
    methods: {
        getReadings() {
            axios.get('/readings').then(response => {
                response.data.forEach(reading => {
                    this.sensorData.labels.push(reading.created_at)
                    this.sensorData.datasets[0].data.push(reading.value)
                });

                // if number of readings exceeds n, filter out older readings
                this.updateReadingsArray();
                this.componentKey++;
            });
        },
        updateReadingsArray(){
          while(this.sensorData.labels.length > this.max_number_of_readings){
              this.sensorData.labels.shift();
              this.sensorData.datasets[0].data.shift();
            }
        }
    }
}
</script>
