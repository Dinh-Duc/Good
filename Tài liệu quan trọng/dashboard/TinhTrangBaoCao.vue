<template>
  <b-card
    v-if="data"
    no-body
    class="card-revenue-budget"
  >
    <b-row class="mx-0">
      <!-- <b-col
        md="6"
        class="revenue-report-wrapper"
      >
        <div class="d-sm-flex justify-content-between align-items-center mb-3">
          <h4 class="card-title mb-50 mb-sm-0">
            Tình trạng báo cáo
          </h4>
          <div class="d-flex align-items-center">
            <div class="d-flex align-items-center mr-2">
              <span
                class="bullet bullet-primary svg-font-small-3 mr-50 cursor-pointer"
              />
              <span>Hoàn thành</span>
            </div>
            <div class="d-flex align-items-center ml-75">
              <span
                class="bullet bullet-warning svg-font-small-3 mr-50 cursor-pointer"
              />
              <span>Trễ hẹn</span>
            </div>
          </div>
        </div>


        <vue-apex-charts
          id="revenue-report-chart"
          type="bar"
          height="230"
          :options="revenueReport.chartOptions"
          :series="data.revenueReport.series"
        />
      </b-col> -->

      <b-col
        md="12"
        class="budget-wrapper pt-1"
      >
        <HopGiaoBan :data="dataChart.meetup" />
      </b-col>
    </b-row>
  </b-card>
</template>

<script>
import {
  BCard, BRow, BCol, BButton,
} from 'bootstrap-vue'
import VueApexCharts from 'vue-apexcharts'
import { $themeColors } from '@themeConfig'
import Ripple from 'vue-ripple-directive'
import HopGiaoBan from './HopGiaoBan.vue'
import SoSanhMucTieu from './SoSanhMucTieu.vue'

export default {
  components: {
    VueApexCharts,
    BCard,
    BButton,
    BRow,
    BCol,
    HopGiaoBan,
    SoSanhMucTieu,
  },
  directives: {
    Ripple,
  },
  props: {
    data: {
      type: Object,
      default: () => {},
    },
  },
  data() {
    return {
      revenueReport: {
        chartOptions: {
          chart: {
            stacked: true,
            type: 'bar',
            toolbar: { show: false },
          },
          grid: {
            padding: {
              top: -20,
              bottom: -10,
            },
            yaxis: {
              lines: { show: false },
            },
          },
          xaxis: {
            categories: ['T1', 'T2', 'T3', 'T4', 'T5', 'T6', 'T7', 'T8', 'T9'],
            labels: {
              style: {
                colors: '#6E6B7B',
                fontSize: '0.86rem',
                /* fontFamily: 'Montserrat', */
              },
            },
            axisTicks: {
              show: false,
            },
            axisBorder: {
              show: false,
            },
          },
          legend: {
            show: false,
          },
          dataLabels: {
            enabled: false,
          },
          colors: [$themeColors.primary, $themeColors.warning],
          plotOptions: {
            bar: {
              columnWidth: '17%',
              endingShape: 'rounded',
            },
            distributed: true,
          },
          yaxis: {
            labels: {
              style: {
                colors: '#6E6B7B',
                fontSize: '0.86rem',
                /* fontFamily: 'Montserrat', */
              },
            },
          },
        },
      },
      // budget chart
      budgetChart: {
        options: {
          chart: {
            height: 80,
            toolbar: { show: false },
            zoom: { enabled: false },
            type: 'line',
            sparkline: { enabled: true },
          },
          stroke: {
            curve: 'smooth',
            dashArray: [0, 5],
            width: [2],
          },
          colors: [$themeColors.primary, '#dcdae3'],
          tooltip: {
            enabled: false,
          },
        },
      },
      dataChart: {
        earningsChart: {
          data: {
            series: [88, 16, 31],
          },
        },
        meetup: {
          avatars: [
            {
              avatar: '/img/avatar-s-9.397f0acd.jpg',
              fullName: 'Billy Hopkins',
            },
            {
              avatar: '/img/avatar-s-6.0f4533ab.jpg',
              fullName: 'Amy Carson',
            },
          ],
          mediaData: [
            {
              avatar: 'CalendarIcon',
              subtitle: '10:AM to 6:PM',
              title: 'Sat, May 25, 2020',
            },
            {
              avatar: 'MapPinIcon',
              subtitle: '2 Nguyễn Văn Trị, Biên Hoà, Đồng Nai',
              title: 'Tầng 7, vp UBND tỉnh',
            },
          ],
        },
      },
    }
  },
}
</script>
<style lang="scss">
.btn-tinhtrang {
  width: 100%;
  float: left;
  margin-bottom: 10px;
}
.btn-tinhtrang button {
  border: unset;
  height: 32px;
  width: 76px;
}
.btn-tinhtrang button:first-child {
  color: white;
  background: #5a8dee;
}
.carousel-caption {
  position: unset !important;
}
.carousel-indicators {
  display: none !important;
}
.btn-group button {
  border-radius: 0px;
}
</style>
