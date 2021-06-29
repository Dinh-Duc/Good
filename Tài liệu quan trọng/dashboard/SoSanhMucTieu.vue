<template>
  <b-card
    v-if="data"
    class="earnings-card cursor-pointer"
    @click="$router.push('apps/bao-cao?id=BCCHUNG')"
  >
    <b-row>
      <b-col cols="7">
        <b-card-title class="mb-1">
          Tình hình giải ngân Bộ Tài nguyên Môi trường
        </b-card-title>
        <!-- <div class="font-small-2">
          Tháng
        </div>
        <h5 class="mb-1">
          4055.56
        </h5> -->
        <b-card-text class="text-muted font-small-3">
          <span>Tổng vốn theo kế hoạch</span>
          <strong class="font-weight-bolder"> 3.176.290 </strong>
          <br>
          <span>Vốn đã giải ngân</span>
          <strong class="font-weight-bolder"> 350.873 </strong>
        </b-card-text>
      </b-col>
      <b-col cols="5">
        <!-- chart -->
        <vue-apex-charts
          height="120"
          :options="earningsChart.chartOptions"
          :series="earningsChart.series"
        />
      </b-col>
    </b-row>
  </b-card>
</template>

<script>
/* eslint-disable */
import {
  BCard, BRow, BCol, BCardTitle, BCardText,
} from 'bootstrap-vue'
import VueApexCharts from 'vue-apexcharts'
import { $themeColors } from '@themeConfig'

const $earningsStrokeColor2 = '#28c76f66'
const $earningsStrokeColor3 = '#28c76f33'
export default {
  components: {
    BCard,
    BRow,
    BCol,
    BCardTitle,
    BCardText,
    VueApexCharts,
  },
  props: {
    data: {
      type: Object,
      default: () => {},
    },
  },
  data() {
    return {
      earningsChart: {
        series: [2077504, 1098786],
        chartOptions: {
          chart: {
            type: 'donut',
            toolbar: {
              show: false,
            },
          },
          dataLabels: {
            enabled: false,
          },
          legend: { show: false },
          comparedResult: [2, -3, 8],
          labels: ['Các vốn khác', 'Địa chất khoáng sản'],
          stroke: { width: 0 },
          colors: [
            $earningsStrokeColor3,
            $themeColors.success,
          ],
          grid: {
            padding: {
              right: -20,
              bottom: -8,
              left: -20,
            },
          },
          plotOptions: {
            pie: {
              startAngle: -10,
              donut: {
                labels: {
                  show: true,
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
                    show: true,
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
                  height: 100,
                },
              },
            },
            {
              breakpoint: 1200,
              options: {
                chart: {
                  height: 120,
                },
              },
            },
            {
              breakpoint: 1045,
              options: {
                chart: {
                  height: 100,
                },
              },
            },
            {
              breakpoint: 992,
              options: {
                chart: {
                  height: 120,
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
