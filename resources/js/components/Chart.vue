<script>
    import { Line } from 'vue-chartjs'

    export default {
        extends: Line,
        // data: () => ({
        //     chartdata: {
        //     labels: ['January', 'February'],
        //     datasets: [
        //         {
        //         label: 'Data One',
        //         backgroundColor: '#f87979',
        //         data: [40, 20]
        //         }
        //     ]
        //     },
        //     options: {
        //     responsive: true,
        //     maintainAspectRatio: false
        //     }
        // }),
        props: {
            chartdata: {
                type: Object,
                default: null
            },
            options: {
                type: Object,
                default: null
            }
        },
        mounted () {
            console.log(this.chartdata)
            this.renderChart(this.chartdata, this.options)
        }
    }
</script>
