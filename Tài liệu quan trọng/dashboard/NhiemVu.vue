<template>
  <b-card
    v-if="data"
    body-class="pb-50"
    class="cursor-pointer"
    @click="$router.push('apps/quan-ly-nhiem-vu')"
  >
    <h6>Nhiệm vụ</h6>
    <h2 class="font-weight-bolder mb-1">
      {{ TotalRows }}
    </h2>
    <!-- chart -->
    <vue-apex-charts
      v-if="TotalRows"
      height="90"
      :options="statisticsOrder.chartOptions"
      :series="statisticsOrder.series"
    />
  </b-card>
</template>

<script>
/* eslint-disable */
import { BCard } from 'bootstrap-vue'
import VueApexCharts from 'vue-apexcharts'
import { $themeColors } from '@themeConfig'

const $barColor = '#f3f3f3'

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
      statisticsOrder: {
        chartOptions: {
          chart: {
            stacked: true,
            type: 'bar',
            toolbar: { show: false },
          },
          colors: ['#ff9f43', '#5A8DEE'],
          grid: {
            show: false,
            padding: {
              left: 0,
              right: 0,
              top: -15,
              bottom: -15,
            },
          },
          plotOptions: {
            bar: {
              horizontal: false,
              columnWidth: '20%',
              startingShape: 'rounded',
              colors: {
                backgroundBarColors: [
                  $barColor,
                  $barColor,
                  $barColor,
                  $barColor,
                  $barColor,
                ],
                backgroundBarRadius: 5,
              },
            },
          },
          legend: {
            show: true,
            position: 'bottom',
            //offsetY: '-10',
            horizontalAlign: 'left',
            fontSize: '8px',
            //height: 30,
            markers: {
              width: 10,
              height: 10,
              radius: 10,
            }
          },
          dataLabels: {
            enabled: false,
          },
          xaxis: {
            labels: {
              show: false,
            },
            categories: ['10/05 - 16/05', '10/05 - 16/05', '10/05 - 16/05', '10/05 - 16/05','10/05 - 16/05'],
            axisBorder: {
              show: false,
            },
            axisTicks: {
              show: false,
            },
          },
          yaxis: {
            show: false,
          },
          tooltip: {
            x: {
              show: true,
            },
          },
          budgetChart: {
            colors: ['#ff9f43', '#5A8DEE'],
          },
        },
        series: [
          {
            data: [4, 5, 9, 20, 5],
            name: 'Chưa thực hiện',
          },
          {
            data: [13, 20, 40, 30, 10],
            name: 'Đã thực hiện',
          },
        ],
      },
      TotalRows: 100,
    }
  },
  created() {
    // COMMON_POST2('http://btnmt-qlnvbe.chinhquyendientu.vn/api/qlnv/nhiem-vu/get-all',
    //   {
    //     ChuyenVienTheoDoi: '',
    //     DaGuiVPCP: null,
    //     DonViQuaHanId: null,
    //     DonViTheoDoi: '',
    //     HanXuLy: null,
    //     HanXuLyVPCP: null,
    //     Index: 1,
    //     IsNhiemVuCaNhan: 'false',
    //     KeySearch: '',
    //     LoaiNhiemVuId: null,
    //     NgayHoanThanh: null,
    //     NgayVanBan: null,
    //     NguoiGiaoViec: '',
    //     NoiDungTheoDoi: '',
    //     NoiDungThuHoi: '',
    //     NoiDungTraLai: '',
    //     NoiDungYKien: '',
    //     Size: 1,
    //     SoKyHieuVanBan: '',
    //     SoNhiemVu: '',
    //     TenDonViCaNhanBiDonDoc: '',
    //     TenDonViCaNhanThuHoi: '',
    //     TenDonViCaNhanTraLai: '',
    //     ThoiGianDonDoc: null,
    //     TinhHinhThucHien: '',
    //     TrangThaiHanXuLy: null,
    //     TrangThaiId: null,
    //     TrichYeuVanBan: '',
    //   },
    // ).then(res => {
    //   this.TotalRows = res.TotalRows
    // })
  },
}
</script>
