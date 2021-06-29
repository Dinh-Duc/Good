<template>
  <b-card
    v-if="data"
    class="card-tiny-line-stats"
    style="cursor: pointer"
    body-class=""
    @click="$router.push('/apps/quan-ly-van-ban')"
  >
    <h6>Văn bản cần xử lý</h6>
    <h2 class="font-weight-bolder mb-1">
      2774
    </h2>
    <!-- chart -->
    <vue-apex-charts
      height="70"
      :options="statisticsProfit.chartOptions"
      :series="[
        {
          name: 'Số văn bản cần xử lý',
          data: [200, 100, 300, 150, 650],
        },
      ]"
    />
  </b-card>
</template>

<script>
/* eslint-disable */

import { BCard } from 'bootstrap-vue'
import VueApexCharts from 'vue-apexcharts'
import { $themeColors } from '@themeConfig'

const $trackBgColor = '#EBEBEB'

export default {
  components: {
    BCard,
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
      statisticsProfit: {
        chartOptions: {
          chart: {
            type: 'line',
            toolbar: {
              show: false,
            },
            zoom: {
              enabled: false,
            },
          },
          grid: {
            borderColor: $trackBgColor,
            strokeDashArray: 5,
            xaxis: {
              lines: {
                show: true,
              },
            },
            yaxis: {
              lines: {
                show: false,
              },
            },
            padding: {
              top: -30,
              bottom: -10,
            },
          },
          stroke: {
            width: 3,
          },
          colors: [$themeColors.info],
          markers: {
            size: 2,
            colors: $themeColors.info,
            strokeColors: $themeColors.info,
            strokeWidth: 2,
            strokeOpacity: 1,
            strokeDashArray: 0,
            fillOpacity: 1,
            discrete: [
              {
                seriesIndex: 0,
                dataPointIndex: 5,
                fillColor: '#ffffff',
                strokeColor: $themeColors.info,
                size: 5,
              },
            ],
            shape: 'circle',
            radius: 2,
            hover: {
              size: 3,
            },
          },
          xaxis: {
            labels: {
              show: true,
              style: {
                fontSize: '0px',
              },
            },
            axisBorder: {
              show: false,
            },
            axisTicks: {
              show: false,
            },
            categories: ['24/6 - 30/6', '14/6 - 20/6', '31/6 - 6/6', '7/6 - 13/6', '14/6 - 20/6'],
          },
          yaxis: {
            show: false,
          },
          tooltip: {
            x: {
              show: false,
            },
          },
        },
      },
    }
  },
  created() {
    // COMMON_POST2('http://45.117.83.218:5004/api/VanBan/count_van_ban', {
    //   fromNgayDen: '01/01/2021 00:00:00',
    //   fromNgayVB: '',
    //   keyword: '',
    //   loaiVanBan: -1,
    //   maTinhTrang: '',
    //   maTrangThai: 'Chưa xử lý',
    //   noiBanHanh: '',
    //   noiNhan: '',
    //   pageIndex: 1,
    //   pageSize: 50,
    //   timeFormat: 'dd/MM/yyyy HH:mm:ss',
    //   toNgayDen: '31/12/2021 00:00:00',
    //   toNgayVB: '',
    // }).then(res => {
    //   console.log(res)
    // })
  },
}
</script>
