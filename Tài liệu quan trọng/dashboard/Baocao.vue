<template>
  <b-card
    no-body
    class="card-browser-states"
  >
    <b-card-header style="padding-bottom: 0">
      <div>
        <b-card-title>Báo cáo chuyên ngành</b-card-title>
        <b-card-text class="font-small-2">
          <!-- 3 tháng gần nhất 2021 -->
        </b-card-text>
      </div>
    </b-card-header>

    <!-- body -->
    <b-card-body>
      <div class="content minor-icon-contaniner hash_clas_caskj124">
        <div class="row mb-2">
          <div class="text-center col-4 col-md-4">
            <div class="cursor-pointer ct-item">
              <img
                src="@/assets/images/dashboard2/dia_chat_ks.22d49d4a.png"
                alt="A"
              >
              <p>
                Địa chất <br>
                khoáng sản
              </p>
            </div>
          </div>
          <div class="text-center col-4 col-md-4">
            <div class="cursor-pointer ct-item">
              <img
                src="@/assets/images/dashboard2/bien_haidao.4cdc1188.png"
                alt=""
              >
              <p>
                Biển Hải<br>
                đảo
              </p>
            </div>
          </div>
          <div class="text-center col-4 col-md-4">
            <div class="cursor-pointer ct-item">
              <img
                src="@/assets/images/dashboard2/dat_dai.b81fc6d8.png"
                alt=""
              >
              <p>
                Thực hiện<br>
                nhiệm vụ
              </p>
            </div>
          </div>
        </div>
        <div class="row mb-2">
          <div class="text-center col-4 col-md-4">
            <a><div class="cursor-pointer ct-item">
              <img
                src="@/assets/images/dashboard2/TN_nuoc.998706a3.png"
                alt=""
              >
              <p>
                Tài nguyên<br>
                nước
              </p>
            </div></a>
          </div>
          <div class="text-center col-4 col-md-4">
            <a><div class="cursor-pointer ct-item">
              <img
                src="data:image/png;base64,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"
                alt=""
              >
              <p>Môi trường</p>
            </div></a>
          </div>
          <div class="text-center col-4 col-md-4">
            <a><div class="cursor-pointer ct-item">
              <img
                src="@/assets/images/dashboard2/khi_tuong.png"
                alt=""
              >
              <p>
                Khí tượng <br>
                thủy văn
              </p>
            </div>
            </a>
          </div>
        </div>
        <div class="row mb-2">
          <div class="text-center col-4 col-md-4">
            <a><div class="cursor-pointer ct-item">
              <img
                src="@/assets/images/dashboard2/vien_tham.png"
                alt=""
              >
              <p>Viễn thám</p>
            </div></a>
          </div>
          <div class="text-center col-4 col-md-4">
            <a><div class="cursor-pointer ct-item">
              <img
                src="@/assets/images/dashboard2/bien_doi.svg"
                alt=""
              >
              <p>Biến đổi<br>khí hậu</p>
            </div></a>
          </div>
          <div class="text-center col-4 col-md-4">
            <a><div class="cursor-pointer ct-item">
              <img
                src="@/assets/images/dashboard2/do_bando.50f189cc.png"
                alt=""
                class="img-fluid"
              >
              <p>Đo đạc<br>bản đồ</p>
            </div></a>
          </div>
        </div>
      </div>
      <!-- <div
        v-for="(browser, index) in browserData"
        :key="index"
        class="browser-states"
      >
        <b-media no-body>
          <b-media-aside class="mr-1 max-w-22">
            <b-img
              :src="browser.imgAvtBaoCao"
              fluid
              alt="browser img"
            />
          </b-media-aside>
          <b-media-body>
            <h6 class="align-self-center my-auto">
              {{ browser.name }}
            </h6>
          </b-media-body>
        </b-media>
        <div class="d-flex align-items-center">
          <span class="font-weight-bold text-body-heading mr-1">{{
            browser.usage
          }}</span>
          <vue-apex-charts
            type="radialBar"
            height="30"
            width="30"
            :options="chartData[index].options"
            :series="chartData[index].series"
          />
        </div>
      </div> -->
    </b-card-body>
    <!--/ body -->
  </b-card>
</template>

<script>
/* eslint-disable */
import {
  BCard,
  BCardHeader,
  BCardTitle,
  BCardText,
  BCardBody,
  BMedia,
  BMediaAside,
  BMediaBody,
  BImg,
  BDropdown,
  BDropdownItem,
} from 'bootstrap-vue'
import VueApexCharts from 'vue-apexcharts'
import { $themeColors } from '@themeConfig'
/* eslint-disable global-require */
const $trackBgColor = '#e9ecef'
export default {
  components: {
    BCard,
    BCardHeader,
    BCardTitle,
    BCardText,
    BCardBody,
    BMedia,
    BMediaAside,
    BMediaBody,
    BImg,
    BDropdown,
    BDropdownItem,
    VueApexCharts,
  },
  data() {
    return {
      chartData: [],
      chartClone: {},
      chartColor: [
        $themeColors.primary,
        $themeColors.warning,
        $themeColors.secondary,
        $themeColors.info,
        $themeColors.danger,
        $themeColors.danger,
      ],
      chartSeries: [],
      browserData: [
        {
          imgAvtBaoCao: require('@/assets/images/dashboard2/dia_chat_ks.22d49d4a.png'),
          name: 'Địa chất khoáng sản',
          // usage: '54.4%',
          imgChart: require('@/assets/images/dashboard2/thuChiNS.png'),
        },
        {
          imgAvtBaoCao: require('@/assets/images/dashboard2/bien_haidao.4cdc1188.png'),
          name: 'Biển & Hải đảo',
          // usage: '6.1%',
          imgChart: require('@/assets/images/dashboard2/dautuCong.png'),
        },
        {
          imgAvtBaoCao: require('@/assets/images/dashboard2/dat_dai.b81fc6d8.png'),
          name: 'Thực hiện nhiêm vụ',
          // usage: '14.6%',
          imgChart: require('@/assets/images/dashboard2/dkDoangNghiep.png'),
        },
        {
          imgAvtBaoCao: require('@/assets/images/dashboard2/TN_nuoc.998706a3.png'),
          name: 'Tài nguyên nước',
          // usage: '4.2%',
          imgChart: require('@/assets/images/dashboard2/xuatNhapKhau.png'),
        },
        {
          imgAvtBaoCao: require('@/assets/images/dashboard2/download.png'),
          name: 'Môi trường',
          // usage: '8%',
          imgChart: require('@/assets/images/dashboard2/dauTuTrongNuoc.png'),
        },
        {
          imgAvtBaoCao: require('@/assets/images/dashboard2/khi_tuong.png'),
          name: 'Khí tượng thủy văn',
          // usage: '8%',
          imgChart: require('@/assets/images/dashboard2/dauTuNgoaiNuoc.png'),
        },
        {
          imgAvtBaoCao: require('@/assets/images/dashboard2/vien_tham.png'),
          name: 'Viễn thám',
          // usage: '8%',
          imgChart: require('@/assets/images/dashboard2/dauTuNgoaiNuoc.png'),
        },
        {
          imgAvtBaoCao: require('@/assets/images/dashboard2/bien_doi.svg'),
          name: 'Biến đổi khí hậu',
          // usage: '8%',
          imgChart: require('@/assets/images/dashboard2/dauTuNgoaiNuoc.png'),
        },
        {
          imgAvtBaoCao: require('@/assets/images/dashboard2/do_bando.50f189cc.png'),
          name: 'Đo đạc bản đồ',
          // usage: '8%',
          imgChart: require('@/assets/images/dashboard2/dauTuNgoaiNuoc.png'),
        },
      ],
      chart: {
        series: [65],
        options: {
          grid: {
            show: false,
            padding: {
              left: -15,
              right: -15,
              top: -12,
              bottom: -15,
            },
          },
          colors: [$themeColors.primary],
          plotOptions: {
            radialBar: {
              hollow: {
                size: '22%',
              },
              track: {
                background: $trackBgColor,
              },
              dataLabels: {
                showOn: 'always',
                name: {
                  show: false,
                },
                value: {
                  show: false,
                },
              },
            },
          },
          stroke: {
            lineCap: 'round',
          },
        },
      },
    }
  },
  created() {
    for (let i = 0; i < this.browserData.length; i += 1) {
      const chartClone = JSON.parse(JSON.stringify(this.chart))
      chartClone.options.colors[0] = this.chartColor[i]
      chartClone.series[0] = this.chartSeries[i]
      this.chartData.push(chartClone)
    }
  },
}
</script>

<style lang="scss" scoped>
.content {
  .minor-icon-contaniner.hash_clas_caskj124 {
    width: 100%;
    margin: .5em 0 0 0;
    padding-top: 10px;

    p {
      margin-bottom: 0;
    }
  }
}
.browser-states {
  margin-top: 1.14rem !important;
}
.max-w-22 {
  max-width: 30px;
}

</style>
