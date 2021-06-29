<template>
  <b-card class="h-100">
    <b-col cols="12">
      <div>
        <h4 class="card-title">
          Cơ cấu trữ lượng khoáng sản đã cấp phép
        </h4>
      </div>
      <!-- chart -->
      <div class="d-flex flex-column h-100 w-100 justify-content-center align-items-center">
        <vue-apex-charts
          height="300"
          width="300"
          :options="earningsChart.chartOptions"
          :series="earningsChart.series"
        />
      </div>
    </b-col>
  </b-card>
</template>

<script>
/* eslint-disable */
import {
  BCard, BRow, BCol, BCardTitle, BCardText,
} from 'bootstrap-vue'
import VueApexCharts from 'vue-apexcharts'

export default {
  components: {
    BCard,
    BRow,
    BCol,
    BCardTitle,
    BCardText,
    VueApexCharts,
  },
  data() {
    return {
      earningsChart: {
        series: [16.43, 83.57],
        chartOptions: {
          chart: {
            type: 'donut',
            toolbar: {
              show: true,
              formatter(val) {
                // eslint-disable-next-line radix
                console.log(val)
                return `${val}%`
              },
            },
            colors: [
                'green',
                '#666',
            ],
          },
          dataLabels: {
            enabled: true,
          },
          legend: {
            show: true,
            position: 'bottom',
          },
          comparedResult: [2, -3, 8],
          labels: ['Đã khai thác', 'Còn lại'],
          stroke: { width: 0 },
          colors: [
            'rgb(40, 199, 111)',
            'rgb(168, 68, 50)',
          ],
        //   grid: {
        //     padding: {
        //       right: -20,
        //       bottom: -8,
        //       left: -20,
        //     },
        //   },
          plotOptions: {
            pie: {
              startAngle: -10,
              donut: {
                labels: {
                  show: false,
                  name: {
                    offsetY: 15,
                  },
                  value: {
                    offsetY: -15,
                    formatter(val) {
                      // eslint-disable-next-line radix
                      return `${parseFloat(val / (3176290 / 100)).toFixed(1)}%`
                    },
                  },
                  total: {
                    show: false,
                    offsetY: 15,
                    label: 'Địa chất khoáng sản',
                    formatter() {
                      return '34,6%'
                    },
                  },
                },
              },
            },
          },
          responsive: [
            {
              breakpoint: 1325,
              options: {
                chart: {
                  height: 280
                },
              },
            },
            {
              breakpoint: 1200,
              options: {
                chart: {
                  height: 300,
                },
              },
            },
            {
              breakpoint: 1044,
              options: {
                chart: {
                  height: 280,
                },
              },
            },
            {
              breakpoint: 991,
              options: {
                chart: {
                  height: 280,
                },
              },
            },
          ],
        },
      },
    }
  },
}
</script>

<style lang="scss" scoped>
.earnings-card {
  .font-weight-bolder {
    color: #40566f;
    font-size: medium;
  }
}
</style>
