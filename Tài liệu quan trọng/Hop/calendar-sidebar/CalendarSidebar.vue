<template>
  <div class="sidebar-wrapper">
    <vue-perfect-scrollbar
      :settings="perfectScrollbarSettings"
      class="scroll-area"
    >
      <div class="sidebar-wrapper__calander">
        <div class="sidebar-calander__actions">
          <div class="sidebar-calander__actions-wrapper">
            <div
              class="d-flex align-items-center justify-content-center add-event space-x-10 cursor-pointer"
              @click="$bvModal.show('modal-event-add')"
            >
              <svg
                v-svg
                symbol="icon-plus"
                size="12 12"
              />
              <span>Đăng ký</span>
            </div>
          </div>
          <div>
            <v-calendar
              ref="view-calendar"
              is-range
              is-expanded
              :attributes="attrs"
              :masks="masks"
              :first-day-of-week="2"
              trim-weeks
              locale="vi"
              title-position="left"
              :disable-page-swipe="false"
              @dayclick="onDayClick"
            />
          </div>
        </div>
        <div class="sidebar-calander__find flex items-center">
          <div
            class="absolute sidebar-calander__find-btn cursor-pointer text-main"
          >
            <svg
              v-svg
              symbol="icon-search"
              size="20 20"
            />
          </div>
          <input
            v-model="search_user"
            class="w-full"
            placeholder="Tìm theo người"
          >
        </div>
        <div class="sidebar-calander__filter">
          <div
            class="event-filter d-flex align-items-center pr-2"
            :class="{ active: isActiveLeftSideBarHop === 'personal' }"
            @click="
              actionLeftSideBar('personal')
              $store.dispatch('hop/actionIsActiveLeftSideBarHop', 'personal')
            "
          >
            <svg
              v-svg
              symbol="icon-user"
              size="12 12"
            />
            <span class="ml-1">Lịch họp của tôi</span>
            <b-badge
              v-if="MeetingCounter.length"
              pill
              class="ml-auto pr-2"
            >
              {{ MeetingCounter[0].count }}
            </b-badge>
          </div>
          <div
            class="event-filter d-flex align-items-center pr-2"
            :class="{ active: isActiveLeftSideBarHop === 'unit' }"
            @click="
              actionLeftSideBar('unit')
              $store.dispatch('hop/actionIsActiveLeftSideBarHop', 'unit')"
          >
            <div class="w-10">
              <svg
                v-svg
                symbol="icon-unit"
                size="14 14"
              />
            </div>
            <span class="ml-1">Đơn vị</span>
            <b-badge
              v-if="MeetingCounter.length"
              pill
              class="ml-auto pr-2"
            >
              {{ MeetingCounter[1].count }}
            </b-badge>
          </div>
          <div class="mt-2 w-100">
            <h5 class="app-label">
              <span class="align-middle">Đơn vị</span>
            </h5>
            <div class="box-donvi-hop align-items-center justify-content-start style-scroll--t d-flex flex-column w-100 pr-2">
              <ItemChild
                v-for="item in filterUnitEvent"
                :key="item.tenDonVi"
                :class="{ active: isActiveLeftSideBarHop === item.id }"
                :data-menu="item"
              />
            </div>
          </div>
          <div class="mt-2">
            <h5 class="app-label">
              <span class="align-middle">Phòng họp trực tuyến</span>
            </h5>
            <div
              v-for="item in sidebarHopTrucTuyen"
              :key="item.name"
              class="event-filter d-flex align-items-center"
              :class="{ active: isActiveLeftSideBarHop === item.id }"
              @click="
                $store.dispatch('hop/actionIsActiveLeftSideBarHop', item.id)
                openPhongHop(item.link)
              "
            >
              <svg
                v-svg
                symbol="icon-layer"
                size="12 12"
              />
              <span class="ml-1">{{ item.name }}</span>
            </div>
          </div>
        </div>
      </div>
    </vue-perfect-scrollbar>
  </div>
</template>

<script>
/* eslint-disable */
import { BBadge } from 'bootstrap-vue'
import Ripple from 'vue-ripple-directive'
import { mapGetters } from 'vuex'
import useCalendarSidebar from './useCalendarSidebar'
import { listAndCountDonVi, apiCountLichCuaDonVi } from '@/api/hop/indexNew'
import moment from 'moment'
import { USER_DATA } from '@/configs/config.js'

export default {
  directives: {
    Ripple,
  },
  components: {
    BBadge,
    VuePerfectScrollbar: () => import('vue-perfect-scrollbar'),
    ItemChild: () => import('./ItemChild.vue'),
  },
  props: {
    isEventHandlerSidebarActive: {
      type: Boolean,
      require: true,
    },
    isEventHandlerAddActive: {
      type: Boolean,
      default: false,
    },
    events: {
      type: Array,
      default: null,
    },
    calendarApi: {
      type: Object,
      default: null,
    },
  },
  data() {
    return {
      paramPayload: {
        CanBoId: '',
        Loai: -1,
        PageIndex: 1,
        PageSize: 15,
        orderBy: 'ThoiGian',
        orderType: false,
        DateStart: moment()
        .subtract(0, 'months')
        .startOf('month')
        .format('YYYY-MM-DD'),
        DateTo: moment()
        .subtract(0, 'months')
        .endOf('month')
        .format('YYYY-MM-DD'),
      },
      activeDate: undefined,
      isActiveMenu: '',
      perfectScrollbarSettings: {
        maxScrollbarLength: 150,
      },
      masks: {
        title: 'MMMM, YYYY',
      },
      search_user: '',
      filterSelect: 'personal',
      filterUnitEvent: [
        {
          tenDonVi: 'Hội đồng thành viên',
          id: 'hdtv_1',
          count: '1'
        },
        {
          tenDonVi: 'Ban kiểm soát',
          id: 'hdtv_2',
          count: '1'
        },
        {
          tenDonVi: 'Ban điều hành',
          id: 'hdtv_3',
          count: '1'
        }
      ],
      sidebarHopTrucTuyen: [
        {
          name: 'Họp giao ban tuần',
          id: 'type_1',
          count: '1',
          link:
            'https://call.chinhquyendientu.vn/UBND-DN-HOP-thuong-truc-tinh-uy',
        },
        // {
        //   name: 'Họp thường trực ủy ban (7/7)',
        //   id: 'type_2',
        //   count: '1',
        //   link:
        //     'https://call.chinhquyendientu.vn/UBND-DN-HOP-thuong-truc-uy-ban',
        // },
        // {
        //   name: 'Họp BCĐ phòng chống covid (16/19)',
        //   id: 'type_3',
        //   count: '1',
        //   link:
        //     'https://call.chinhquyendientu.vn/UBND-DN-HOP-bcd-phong-chong-covid',
        // },
      ],
    }
  },
  computed: {
    markdates() {
      // eslint-disable-next-line no-var
      var arrDate = []
      this.events.forEach(item => {
        arrDate.push(item.end)
        arrDate.push(item.start)
      })
      return arrDate
    },
    attrs() {
      return [
        {
          key: 'today',
          highlight: {
            color: 'red',
            style: {
              background: '#5A8DEE',
              color: 'white',
            },
          },
          dates: new Date(),
        },
        {
          dot: {
            style: {
              backgroundColor: '#46D68C',
            },
          },
          dates: this.markdates,
        },
      ]
    },
    ...mapGetters({
      ListUser: 'hop/ListUser',
      EventPaging: 'hop/EventPaging',
      isActiveLeftSideBarHop: 'hop/isActiveLeftSideBarHop',
      MeetingCounter: 'hop/MeetingCounter',
    }),
  },
  created() {
    // this.render()
    // this.getCountDonVi()
  },
  watch: {
    ListUser: {
      handler(val){
        if(val){
          // this.actionLeftSideBar('unit')
        }
      }
    }
  },
  methods: {
    actionLeftSideBar(val){
      switch(val){
        case 'personal':
          this.actionGetPersonal()
          break
        case 'unit':
          this.actionGetUnit()
          break
        default:
          return
      }

    },
    actionGetPersonal(){
      const tmp_payload = Object.assign({}, this.paramPayload)
      tmp_payload.Loai = -1
      tmp_payload.DonViId = null
      tmp_payload.canBoId = JSON.parse(localStorage.getItem(USER_DATA)).id.toString()
      this.actionCountMeetingPersonal(tmp_payload)
    },
    actionGetUnit(){
      const tmp_payload = Object.assign({}, this.paramPayload)
      const item_IdCanBo = this.ListUser.filter(element => element.value.CanBoId == JSON.parse(localStorage.getItem(USER_DATA)).id.toString())

      if(item_IdCanBo.length > 0){
        tmp_payload.DonViId = item_IdCanBo[0].value.iD_DonVi
      }
      tmp_payload.Loai = 1
      tmp_payload.canBoId = null
      this.actionCountMeetingUnit(tmp_payload)
    },
    actionCountMeetingPersonal(val){
      this.$store.dispatch('hop/getListEvents', val)
    },
    actionCountMeetingUnit(val){
      this.$store.dispatch('hop/getListEvents', val)
    },
    getCountDonVi(){
      const payload = {}
      listAndCountDonVi(payload)
      .then(data => {
        if(data.succeeded){
          if(data.data.length > 0){
            const payloadChild = {
              DonViId: data.data[0].id
            }
            listAndCountDonVi(payloadChild)
            .then(data => {
              if(data.succeeded){
                this.filterUnitEvent = data.data
              }
            })
            .catch(err => {
              console.log(err)
            })
          }
        }
      })
      .catch(err => {
        console.log(err);
      })
    },
    openPhongHop(link) {
      window.open(link)
    },
    onDayClick(day) {
      this.calendarApi.gotoDate(day.id)
      if (this.calendarApi.view.type.indexOf('list') !== -1) {
        this.calendarApi.changeView('listDay')
        this.$emit('typeView', 'list')
      } else {
        this.calendarApi.changeView('timeGridDay')
        this.$emit('typeView', 'grid')
      }
      this.$emit('changeTitle', this.calendarApi.view.title)
      this.$emit('timeSelect', 'day')
    },
    render() {
      this.filterUnitEvent.length = 0
      apiCountLichCuaDonVi({
        canBoId: JSON.parse(localStorage.getItem('userData')).id,
      }).then(response => {
        response.data.map(item => {
          this.filterUnitEvent.push({
            name: item.tenDonVi,
            id: item.id,
            count: item.tongSoLich,
          })
          return null
        })
      })
    },
  },
  setup() {
    const {
      calendarOptions,
      selectedCalendars,
      checkAll,
    } = useCalendarSidebar()

    return {
      calendarOptions,
      selectedCalendars,
      checkAll,
    }
  },
}
</script>
<style lang="scss">
.height-sidebar {
  height: 37vh;
}
</style>
