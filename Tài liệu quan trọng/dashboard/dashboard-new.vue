<template>
  <div class="box-dashbroard2">
    <b-row>
      <b-col
        sm="12"
        md="6"
        lg="7"
        xl="7"
        class="col-fh-9 col-hd-8"
      >
        <div class="box-thoigian d-flex align-items-center">
          <div class="box-thoigian-left">
            <span>{{ time }}</span>
          </div>
          <div class="box-nhietdo">
            <div class="box-nhietdo-gia-tri">
              <div>
                <img src="@/assets/images/icons/weather.svg">
                <span>{{ temperature }}°C</span>
              </div>

              <span class="box-nhietdo__right-value">AQI: </span>
              <span class="text-success">49 (Tốt)</span>
            </div>
          </div>
          <div class="box-thoigian-right">
            <p>{{ dateNow }}</p>
            <div class="box-thoigian-lich-am">
              <span>{{ moonDate }}</span>
              <svg
                width="6"
                height="6"
                viewBox="0 0 6 6"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <circle
                  cx="3"
                  cy="3"
                  r="3"
                  fill="#FFA902"
                />
              </svg>
              <span> Ngày Hoàng đạo </span>
            </div>
          </div>
        </div>
      </b-col>
      <b-col
        sm="12"
        md="6"
        lg="5"
        xl="5"
        class="col-fh-3 col-hd-4"
        style="padding-top: 20px;"
      >
        <!-- <div class="box-nhietdo">
          <div class="box-nhietdo-gia-tri">
            <img src="@/assets/images/icons/weather.svg">
            <span>{{ temperature }}°C</span>
            <span
              class="box-nhietdo__right-value"
            >AQI: <span class="text-success">49 (Tốt)</span></span>
          </div>
          <div class="tabs-ngay-thang-nam">
            <b-button-group class="mt-1">
              <div class="btn-group">
                <b-button
                  :class="btnActive == 0 ? 'active' : ''"
                  variant="primary"
                  @click="active(0)"
                >
                  Ngày
                </b-button>
              </div>
              <div class="btn-group">
                <b-button
                  :class="btnActive == 1 ? 'active' : ''"
                  variant="primary"
                  @click="active(1)"
                >
                  Tuần
                </b-button>
              </div>
              <div class="btn-group">
                <b-button
                  :class="btnActive == 2 ? 'active' : ''"
                  variant="primary"
                  @click="active(2)"
                >
                  Tháng
                </b-button>
              </div>
            </b-button-group>
          </div>
        </div> -->

        <user-dropdown style="float: right" />
        <div style="float: right; width: 50px;">
          <notification-dropdown
            class="notifi-dasboard"
            style="padding-top: 10px; float: right;"
          />
        </div>
      </b-col>
    </b-row>

    <b-row
      class="match-height spacing-15"
      style="margin-top: 20px"
    >
      <b-col lg="4">
        <b-row class="match-height spacing-15">
          <!-- Bar Chart - Orders -->
          <b-col
            lg="12"
            md="6"
            cols="6"
          >
            <NhiemVu :data="dataChart.statisticsOrder" />
          </b-col>
          <!--/ Bar Chart - Orders -->
          <b-col
            lg="12"
            md="6"
            cols="6"
          >
            <VanBanCanXuLy :data="dataChart.statisticsProfit" />
          </b-col>

        </b-row>
      </b-col>

      <b-col lg="8" class="d-flex flex-row card">
        <b-col
          lg="6"
          md="6"
        >
          <SoSanhMucTieu :data="dataChart.earningsChart" />
          <SoSanhMucTieu2 :data="dataChart.earningsChart" />
        </b-col>
        <b-col
          lg="6"
          md="6"
        >
          <TinhTrangBaoCao :data="dataChart.revenue" />
        </b-col>
      </b-col>
    </b-row>

    <b-row class="match-height spacing-15">
      <!-- Company Table Card -->
      <b-col lg="8">
        <DonViTable :table-data="lichlamviec" />
      </b-col>

      <!-- Developer Meetup Card -->
      <b-col
        lg="4"
        md="6"
      >
        <MapAQ />
        <!-- <HopGiaoBan :data="dataChart.meetup" /> -->
      </b-col>
    </b-row>

    <b-row class="match-height spacing-15">
      <b-col
        lg="4"
        md="4"
      >
        <!-- <Baocao /> -->
        <BaoCaoChuyenNghanh />
      </b-col>
      <b-col
        lg="4"
        md="4"
      >
        <YkienNguoiDan :data="dataChart.goalOverview" />
      </b-col>
      <b-col
        lg="4"
        md="4"
      >
        <BaoChi :data="dataChart.transactionData" />
      </b-col>
    </b-row>
  </div>
</template>
<script>
/* eslint-disable */
import store from '@/store'
import moment from 'moment'
import { UrlAPI, USER_DATA } from '@/configs/config'
import UserDropdown from '@core/layouts/components/app-navbar/components/UserDropdown.vue'
import { BRow, BCol, BButtonGroup, BButton, BCard } from 'bootstrap-vue'
import { COMMON_GET } from '@/api/base2'
import { listSchedules } from '@/api/calendar/indexNew'
import NotificationDropdown from '@core/layouts/components/app-navbar/components/NotificationDropdown.vue'

import { mapGetters } from 'vuex'

import TinhTrangBaoCao from './TinhTrangBaoCao.vue'
import NhiemVu from './NhiemVu.vue'
import VanBanCanXuLy from './VanBanCanXuLy.vue'
import SoSanhMucTieu from './SoSanhMucTieu.vue'
import DonViTable from './DonViTable.vue'
/* import DonViTable2 from './DonViTable2.vue' */
import HopGiaoBan from './HopGiaoBan.vue'
import BaoChi from './BaoChi.vue'
import YkienNguoiDan from './YkienNguoiDan.vue'
// import Baocao from './Baocao.vue'
import MapAQ from './MapAQ.vue'

export default {
  name: 'Dashboard',
  components: {
    UserDropdown,
    BRow,
    BCol,
    BButtonGroup,
    BButton,
    BCard,
    moment,
    NotificationDropdown,

    TinhTrangBaoCao,
    NhiemVu,
    VanBanCanXuLy,
    SoSanhMucTieu,
    SoSanhMucTieu2: () => import('./SoSanhMucTieu2.vue'),
    DonViTable,
    HopGiaoBan,
    BaoChi,
    YkienNguoiDan,
    // Baocao,
    MapAQ,
    /* DonViTable2, */
    BaoCaoChuyenNghanh: () => import('./chart-component-child/BaoCaoChuyenNghanh.vue')
  },
  computed: {
    ...mapGetters({
      ListEvents: 'lichlamviec/ListEvents',
    }),
  },
  data() {
    return {
      btnActive: 0,
      currentTime: {
        time: '',
        date: '',
        moonDate: '',
        zodiacDay: '',
      },
      dateNow: '',
      moonDate: '',
      time: '',
      temperature: 0,
      boxDataNv: [],
      lichlamviec: [],

      dataChart: {
        companyTable: [],
        statisticsOrder: {
          series: [
            {
              data: [45, 85, 62, 45, 65],
              name: '2021',
            },
          ],
        },
        statisticsProfit: {
          series: [
            {
              data: [0, 20, 5, , 30, 15, 65],
            },
          ],
        },
        earningsChart: {
          data: {
            series: [88, 16, 31],
          },
        },
        revenue: {
          budget: '56,800',
          price: '25,852',
          budgetChart: {
            series: [
              {
                data: [61, 48, 49, 52, 64, 40, 79, 60, 59, 43, 62],
              },
              {
                data: [20, 10, 30, 15, 23, 0, 25, 15, 20, 5, 27],
              },
            ],
          },
          revenueReport: {
            series: [
              {
                data: [95, 177, 284, 256, 105, 63, 168, 218, 72],
                name: 'Earning',
              },
              {
                data: [-145, -80, -60, -280, -100, -60, -85, -75, -100],
                name: 'Expense',
              },
            ],
          },
          years: ['2019', '2020', '2021'],
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
        goalOverview: {
          completed: '786,617',
          inProgress: '13,561',
          series: [83],
        },
        transactionData: [
          {
            avatar: require('@/assets/images/dashboard2/baochi.svg'),
            avatarVariant: 'light-primary',
            payment: 200,
            mode: 'Báo chí',
          },
          {
            avatar: require('@/assets/images/dashboard2/facebook.svg'),
            avatarVariant: 'light-success',
            payment: 60,
            mode: 'Mạng xã hội',
          },
          {
            avatar: require('@/assets/images/dashboard2/blog.svg'),
            payment: 16,
            mode: 'Blog',
          },
          {
            avatar: require('@/assets/images/dashboard2/forum.svg'),
            avatarVariant: 'light-warning',
            payment: 500,
            mode: 'Forum',
          },
          {
            avatar: require('@/assets/images/dashboard2/other.svg'),
            avatarVariant: 'light-info',
            payment: 30,
            mode: 'Nguồn khác',
          },
        ],
      },
    }
  },
  beforeCreate() {
    store.commit('appConfig/UPDATE_NAVBAR_CONFIG', { type: 'hidden' })
    store.commit('appConfig/UPDATE_FOOTER_CONFIG', { type: 'hidden' })
  },
  created() {
    COMMON_GET(
      'https://ubndtinhdongnai-be.chinhquyendientu.vn/api/LunarDate/getLunarDate',
    ).then(res => {
      this.dateNow = res.resultObj.dateMore
      this.moonDate = res.resultObj.lunarDateArray[0]
    })

    COMMON_GET(
      'https://ubndtinhdongnai-be.chinhquyendientu.vn/api/AreaWeather/getweatherbycode',
      { code: setLocaltion },
    ).then(res => {
      if (res.resultObj.current) {
        this.temperature = Math.ceil(res.resultObj.current.temp.day)
      } else {
        this.temperature = 32
      }
    })
    this.getTimeNow()
    // this.getDocs()
    // this.getDataNv()
    this.getListScheduleInMonth()
  },
  mounted() {},
  beforeDestroy() {
    store.commit('appConfig/UPDATE_NAVBAR_CONFIG', { type: 'sticky' })
  },
  methods: {
    active(number) {
      this.btnActive = number
    },
    route(url) {
      console.log(url)
      this.$router.push({ name: url })
    },
    toggleVerticalMenuActive() {
      /* document.querySelector.classList.remove(); */
    },
    getTimeNow() {
      let current = new Date()
      this.time = `${current.getHours()}:${this.forMatMinute(
        current.getMinutes(),
      )}`
      setTimeout(() => {
        this.time = `${current.getHours()}:${this.forMatMinute(
          current.getMinutes(),
        )}`
        this.getTimeNow()
      }, 1000)
    },
    forMatMinute(number) {
      const minute = number.toString().length
      if (minute == 1) {
        return '0' + number
      } else {
        return number
      }
    },
    getDocs() {
      const param = {
        loaiVanBan: 1,
        pageIndex: 1,
        pageSize: 10,
      }

      COMMON_GET(`${UrlAPI}/api/QuanLyVanBan/filter-quanly-vanban`, param).then(
        res => {
          if (res && res.pageData.length > 0) {
            const listPush = []
            for (let index = 0; index < res.pageData.length; index++) {
              const element = {
                icon: require('@/assets/images/icons/ellipse_blue.svg'),
                title:
                  res.pageData[index].soKyHieu +
                  ' ' +
                  res.pageData[index].ngayNhan +
                  ' ' +
                  res.pageData[index].trichYeu,
                url: '#',
              }
              listPush.push(element)
            }

            // this.leftData = this.leftData.map(x => {
            //   if (x.id === 2) {
            //     x.data = listPush
            //   }
            //   return x
            // })
          }
        },
      )
    },
    getDataNv() {
      const params = {
        pageIndex: 1,
        pageSize: 12,
      }
      COMMON_GET(
        `${UrlAPI}/api/QuanLyNhiemVu/filter-loai-nhiemvu`,
        params,
      ).then(res => {
        const data = []
        if (res.pageData.length > 0) {
          res.pageData.map(item => {
            if (item.noiDung) {
              const dataGet = {
                icon: require('@/assets/images/icons/ellipse.svg'),
                title: item.noiDung,
                url: '#',
              }
              data.push(dataGet)
            }
          })

          // this.leftData = this.leftData.map(x => {
          //   if (x.id === 4) {
          //     x.data = data
          //   }
          //   return x
          // })
        }
      })
    },
    getListScheduleInMonth() {
      const params = {
        DateFrom: moment().startOf("month").format("YYYY-MM-DD"),
        DateTo: moment().endOf("month").format("YYYY-MM-DD"),
        CanBoId: JSON.parse(localStorage.getItem(USER_DATA)).id.toString(),
        Type: -1,
        PageIndex: 1,
        PageSize: 6
      }
      listSchedules(params).then(({
        data,
      }) => {
        if (data) {
          this.lichlamviec = data.items
        }
      }).catch(error => {
        console.log(error)
      })
    }
  },
  filters: {
    DayFormat(value) {
      if (!value) return ''
      const dateval = new Date(value)
      const d = dateval.getDate()
      const m = dateval.getMonth() + 1
      const y = dateval.getFullYear()
      const h = dateval.getHours()
      const minutes = dateval.getMinutes()

      const dateString = `${d <= 9 ? `0${d}` : d}/${
        m <= 9 ? `0${m}` : m
      }/${y} ${h <= 9 ? `0${h}` : h}:${minutes <= 9 ? `0${minutes}` : minutes}`
      return dateString
    },
  },
}
</script>
<style lang="scss">
@import '../../assets/scss/trang-chu.scss';
.notifi-dasboard {
  list-style: none;
  display: flex;
  align-items: center;
  padding: 0.358rem 0.5rem;
  position: relative;
  top: 2px;
  .dropdown-toggle {
    &::after {
      display: none;
    }
  }
  .dropdown-menu-media {
    width: 30rem;
  }
}

.box-dashbroard2 {
  margin-top: -2rem;
}
</style>
