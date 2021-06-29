<template>
  <div
    style="height: inherit"
    class="content-hcc"
  >
    <div
      class="body-content-overlay"
      :class="{ show: mqShallShowLeftSidebar }"
      @click="mqShallShowLeftSidebar = false"
    />
    <div class="todo-app-list">
      <!-- App Searchbar Header -->
      <div class="app-fixed-search d-flex align-items-center">
        <!-- Toggler -->
        <div class="sidebar-toggle d-block d-lg-none ml-1">
          <feather-icon
            icon="MenuIcon"
            size="21"
            class="cursor-pointer"
            @click="mqShallShowLeftSidebar = true"
          />
        </div>
      </div>

      <!-- Todo List -->
      <!-- <vue-perfect-scrollbar
        v-if="!url"
        :settings="perfectScrollbarSettings"
        class="todo-task-list-wrapper list-group scroll-area p-2"
      >
        <b-row>
          <b-col xl="6">
            <b-card class="box-hcc box-border-ml-left">
              <div class="progress-list">
                <div class="mb-1 text-center">
                  <span class="title-progress-hcc">Hồ sơ</span>
                </div>
                <b-progress
                  class="mt-2"
                  :max="progress"
                >
                  <b-progress-bar
                    v-for="(item, index) in dataProgress"
                    :key="index"
                    :style="`background: ${item.color}`"
                    :value="item.value"
                  >
                    <span class="cursor-pointer nut-progress-bar">
                      {{ item.value }}</span>
                  </b-progress-bar>
                </b-progress>
                <b-row class="mx-0 my-2">
                  <b-col
                    v-for="(item, index) in dataProgress"
                    :key="index"
                    xl="4"
                    lg="12"
                    sm="12"
                    class="px-0 d-flex -align-items-center"
                  >
                    <div
                      class="label-progress-hcc"
                      :style="`background: ${item.color}`"
                    />
                    <div>{{ item.status }}</div>
                  </b-col>
                </b-row>
                <div
                  class="border-top progress-status-hc d-flex align-items-center justify-content-center"
                >
                  <div
                    v-for="(item, index) in dataStatus"
                    :key="index"
                    class="status-hc mr-2 py-1"
                  >
                    <div class="cursor-pointer">
                      <span
                        :style="`color: ${item.color}`"
                      >{{ item.value }} </span><span>{{ item.name }}</span>
                    </div>
                  </div>
                </div>
              </div>
            </b-card>
          </b-col>
          <b-col xl="6">
            <b-card class="box-hcc box-hs box-border-ml-left">
              <div class="progress-list">
                <div class="mb-1 text-center">
                  <span
                    class="title-progress-hcc"
                  >Thống kê hồ sơ chưa xử lý theo đơn vị</span>
                </div>
                <b-row
                  v-for="(item, index) in dataHoSo"
                  :key="index"
                  class="mb-2"
                >
                  <b-col
                    xl="4"
                    sm="6"
                  >
                    {{ item.name }}
                  </b-col>
                  <b-col
                    xl="8"
                    sm="6"
                  >
                    <b-progress
                      class="height-30"
                      :value="item.value"
                      :max="item.max"
                      variant="danger"
                      show-value
                    />
                  </b-col>
                </b-row>
              </div>
            </b-card>
          </b-col>
        </b-row>
        <boxTable :data="boxTable" />
      </vue-perfect-scrollbar> -->
      <vue-perfect-scrollbar
        :settings="perfectScrollbarSettings"
        class="todo-task-list-wrapper list-group scroll-area p-2"
      >
        <DashboardHCC v-if="dataSibarMenu.keyParent === 'TONGQUAN'" />
        <Detail
          v-if="checkShowDetail"
          :data-item="dataSibarMenu.dataItem"
        />
      </vue-perfect-scrollbar>
    </div>

    <!-- Sidebar -->
    <portal to="content-renderer-sidebar-left">
      <HanhChinhLeftSibar
        :class="{ show: mqShallShowLeftSidebar }"
        @close-left-sidebar="mqShallShowLeftSidebar = false"
        @dataMenu="dataSibarMenu = $event"
      />
    </portal>
  </div>
</template>
<script>
import VuePerfectScrollbar from 'vue-perfect-scrollbar'
import HanhChinhLeftSibar from './HanhChinhLeftSibar.vue'
import DashboardHCC from './DashboardHCC.vue'
import Detail from './Detail.vue'

export default {
  name: 'HanhChinhCong',
  components: {
    HanhChinhLeftSibar,
    VuePerfectScrollbar,
    Detail,
    DashboardHCC,
  },
  data() {
    return {
      mqShallShowLeftSidebar: false,
      perfectScrollbarSettings: {
        maxScrollbarLength: 150,
      },
      perfectScrollbarProgess: {
        maxScrollbarLength: 30,
      },
      progress: 29,
      url: '',
      dataProgress: [
        {
          value: 10,
          color: '#28a745',
          status: 'Đã xử lý',
        },
        {
          value: 6,
          color: '#ffc107',
          status: 'Chờ xử lý',
        },
        {
          value: 13,
          color: '#17a2b8',
          status: 'Đang xử lý',
        },
      ],
      dataStatus: [
        {
          name: 'Trong hạn',
          value: 8,
          color: '#991EF9',
        },
        {
          name: 'Đến hạn',
          value: 14,
          color: '#06c270',
        },
        {
          name: 'Quá hạn',
          value: 7,
          color: '#ff2929',
        },
      ],
      boxTable: {},
      dataHoSo: [
        {
          name: 'Văn phòng Bộ',
          value: 15,
          max: 60,
        },
        {
          name: 'Sở Kế hoạch và Đầu tư',
          value: 0,
          max: 1,
        },
        {
          name: 'Sở Nông nghiệp và Phát triển Nông thôn',
          value: 0,
          max: 1,
        },
        {
          name: 'Sở Công thương',
          value: 0,
          max: 1,
        },
        {
          name: 'Sở Xây dựng',
          value: 0,
          max: 1,
        },
        {
          name: 'Sở Giao thông vận tải',
          value: 1,
          max: 10,
        },
        {
          name: 'Sở Tài nguyên và Môi trường',
          value: 1,
          max: 1,
        },
        {
          name: 'Sở Khoa học và Công nghệ',
          value: 0,
          max: 1,
        },
        {
          name: 'Sở Giáo dục và Đào tạo',
          value: 0,
          max: 1,
        },
        {
          name: 'Sở Y tế',
          value: 2,
          max: 2,
        },
        {
          name: 'Sở Văn hóa - Thể thao và Du lịch',
          value: 0,
          max: 1,
        },
        {
          name: 'Sở Lao động - Thương binh và Xã hội',
          value: 0,
          max: 1,
        },
        {
          name: 'Sở Tư pháp',
          value: 2,
          max: 2,
        },
        {
          name: 'Sở Thông tin và Truyền thông',
          value: 0,
          max: 1,
        },
        {
          name: 'Sở Nội vụ',
          value: 0,
          max: 1,
        },
        {
          name: 'Sở Ngoại vụ',
          value: 0,
          max: 1,
        },
        {
          name: 'Thanh tra tỉnh',
          value: 0,
          max: 1,
        },
        {
          name: 'Ban quản lý khu công nghệ cao',
          value: 0,
          max: 1,
        },
        {
          name: 'Ban quản lý các khu công nghiệp Đồng Nai',
          value: 0,
          max: 1,
        },
        {
          name: 'Ban Dân tộc',
          value: 0,
          max: 1,
        },
      ],
      dataSibarMenu: {},
    }
  },
  computed: {
    checkShowDetail() {
      if (
        this.dataSibarMenu.keyParent === 'COQUANXULY'
        || this.dataSibarMenu.keyParent === 'TINHTRANGXULY'
      ) {
        return true
      }
      return false
    },
  },
  created() {
    this.$eventBus.$on('data-hcc', data => {
      this.boxStatic = {}
      setTimeout(() => {
        this.boxTable = data.boxTable
        this.url = data.url
      })
    })
  },
}
</script>
<style lang="scss">
@import '~@core/scss/base/pages/app-todo.scss';
.content-hcc {
  .todo-task-list-wrapper {
    height: 100% !important;
  }
  .app-fixed-search {
    border-bottom: 0 !important;
  }
  .card {
    border: 1px solid rgba(71, 95, 123, 0.2);
  }
  .progress-list {
    .title-progress-hcc {
      font-size: 20px;
      font-weight: 600;
    }
  }
  .box-hcc {
    .progress {
      height: 30px;
      border-radius: 5px;
      .progress-bar:last-child {
        border-top-right-radius: 5px;
        border-bottom-right-radius: 5px;
      }
    }
    .label-progress-hcc {
      width: 15px;
      height: 15px;
      margin-right: 8px;
    }
  }
  .box-hcc {
    .card-body {
      height: 233px;
      overflow: hidden;
    }
  }
  .box-hs {
    .card-body {
      overflow-y: scroll;
      &::-webkit-scrollbar {
        display: none;
      }
      &:hover {
        &::-webkit-scrollbar {
          display: block;
        }
      }
      &::-webkit-scrollbar {
        width: 8px;
        background-color: #f5f5f5;
      }
      &::-webkit-scrollbar-thumb {
        border-radius: 8px;
        -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.1);
        background-color: #aaa;
      }
    }
  }
}
</style>
