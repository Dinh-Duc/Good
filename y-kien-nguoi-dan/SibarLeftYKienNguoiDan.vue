<template>
  <div class="sidebar-left">
    <div class="sidebar">
      <div class="sidebar-content todo-sidebar">
        <div class="todo-app-menu sibar-y-kien-nguoidan">
          <vue-perfect-scrollbar
            :settings="perfectScrollbarSettings"
            class="sidebar-menu-list scroll-area py-2"
          >
            <ul class="baocao-task-list menu-lam p-0 m-0">
              <li
                v-for="(item, key) in listNv"
                :key="key"
                class="baocao-item"
              >
                <div
                  :class="{
                    'item d-flex align-items-center': true,
                    active: item.key == keyParentActive,
                  }"
                  @click="showChildReport(item)"
                >
                  <div
                    v-if="item.icon_class"
                    class="icon"
                  >
                    <feather-icon
                      class="mr-1"
                      :icon="item.icon_class"
                      size="14"
                    />
                  </div>
                  <div class="name-parent">
                    {{ item.title }}
                  </div>
                  <div
                    v-if="item.show_total"
                    class="count-item d-flex justify-content-end"
                  >
                    <label class="count">
                      {{ item.total }}
                    </label>
                  </div>
                </div>
                <div class="child-report">
                  <ul
                    v-if="item.childs && item.childs.length > 0"
                    class="mt-0 pl-2"
                  >
                    <li
                      v-for="(item1, key1) in item.childs"
                      :key="key1"
                    >
                      <div
                        :class="{
                          'item d-flex align-items-center': true,
                          active: item1.key == keyChild1Active,
                        }"
                        @click="eventChild(item.key, item1)"
                      >
                        <div
                          v-if="item1.icon_class"
                          class="icon"
                        >
                          <feather-icon
                            class="mr-1"
                            :icon="item1.icon_class"
                            size="14"
                          />
                        </div>
                        <div class="name">
                          {{ item1.title }}
                        </div>
                        <div
                          v-if="item1.show_total"
                          class="count-item d-flex justify-content-end"
                        >
                          <label class="count">
                            {{ item1.total }}
                          </label>
                        </div>
                      </div>
                      <div
                        v-if="
                          item1.childs &&
                            item1.childs.length > 0 &&
                            item1.key == keyChild1Active
                        "
                        class="child-lv-3"
                      >
                        <ul class="mt-0">
                          <li
                            v-for="(item2, key2) in item1.childs"
                            :key="key2"
                          >
                            <div
                              :class="{
                                'item d-flex align-items-center': true,
                                active: item2.key == keyChild2Active,
                              }"
                              @click="eventChild2(item.key, item1, item2)"
                            >
                              <div class="name">
                                {{ item2.title }}
                              </div>
                              <div
                                v-if="item2.show_total"
                                class="count-item d-flex justify-content-end"
                              >
                                <label class="count">
                                  {{ item2.total }}
                                </label>
                              </div>
                            </div>
                          </li>
                        </ul>
                      </div>
                    </li>
                  </ul>
                </div>
              </li>
            </ul>
          </vue-perfect-scrollbar>
          <div class="text-center btn-open-hop-phan">
            <b-button
              variant="primary"
              @click="
                openUrl('http://btnmt-pakn.chinhquyendientu.vn/')
              "
            >
              Ý kiến người dân
            </b-button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { UrlAPI } from '@/configs/config'
import VuePerfectScrollbar from 'vue-perfect-scrollbar'
import datajson from './dataJson.json'

export default {
  components: {
    VuePerfectScrollbar,
  },
  data() {
    return {
      perfectScrollbarSettings: {
        maxScrollbarLength: 60,
      },
      listReport: [
        {
          title: 'Tổng quan',
          key: 'TONGQUAN',
          count: 1,
          childs: [
          ],
          icon: '', // GridIcon
        },
        {
          title: 'Cơ quan xử lý',
          key: 'COQUANXULY',
          count: 0,
          icon: '',
          childs: [
            {
              title: 'Cơ quan thực hiện chức năng quản lý nhà nước',
              key: 'CQTHCNQLNN',
              count: 1,
              icon: 'LayersIcon',
              childs: [
                {
                  title: 'Tổng cục Quản lý đất đai',
                  key: 'TCQLDD',
                  count: 1,
                  childs: [],
                  icon: 'LayersIcon',
                },
              ],

            },
            {
              title: 'Đơn vị sự nghiệp',
              key: 'DVSN',
              count: 1,
              childs: [],
              icon: 'LayersIcon',
            },
            {
              title: 'Các doanh nghiệp',
              key: 'CDN',
              count: 1,
              childs: [],
              icon: 'LayersIcon',
            },
          ],
        },
        {
          title: 'Tình Trạng',
          key: 'TinhTrang',
          count: 0,
          childs: [
            {
              title: 'Chờ xử lý',
              key: 'CHOXULY',
              count: 1,
              childs: [],
              icon: 'LayersIcon',
            },
            {
              title: 'Đang xử lý',
              key: 'DANGXULY',
              count: 1,
              childs: [],
              icon: 'LayersIcon',
            },
            {
              title: 'Đã xử lý',
              key: 'DAXULY',
              count: 1,
              childs: [],
              icon: 'LayersIcon',
            },
            {
              title: 'Quá hạn xử lý',
              key: 'QUAHANXULY',
              count: 1,
              childs: [],
              icon: 'LayersIcon',
            },
          ],
          icon: '',
          dataApi: [],
        },
      ],
      keyParentActive: 'TONGQUAN',
      keyChild1Active: '',
      listNv: datajson,
      keyChild2Active: '',
      dataApi: [],
      dataShow: [],
    }
  },
  created() {
    const form = {
      key: 'TONGQUAN',
      keyChild: '',
    }

    // eslint-disable-next-line no-undef
    COMMON_GET(
      `${UrlAPI}/api/YKienNguoiDan/chitiet-xuly-thaido-congchuc`,
      {},
    ).then(res => {
      this.dataApi = res.data
    })
    this.$eventBus.$emit('dataMenu', form)
  },
  methods: {
    openUrl(url) {
      window.open(url, '_blank')
    },
    showChildReport(item) {
      this.keyParentActive = item.key
      if (item.childs && item.childs.length > 0) {
        this.eventChild(item.key, item.childs[0])
      } else {
        this.keyChild1Active = ''
        this.keyChild2Active = ''
        const form = {
          keyParent: item.key,
          keyChild1: '',
          keyChild2: '',
          dataItem: item.data,
        }
        this.$emit('dataMenu', form)
      }
    },
    eventChild(keyParent, item) {
      this.keyParentActive = keyParent
      this.keyChild1Active = item.key
      if (item.childs && item.childs.length > 0) {
        this.keyChild2Active = item.childs[0].key
        const form = {
          keyParent,
          keyChild1: item.key,
          keyChild2: item.childs[0].key,
          dataItem: item.childs[0].data,
        }
        this.$emit('dataMenu', form)
      } else {
        this.keyChild2Active = ''
        const form = {
          keyParent,
          keyChild1: item.key,
          keyChild2: '',
          dataItem: item.data,
        }
        this.$emit('dataMenu', form)
      }
    },
    eventChild2(keyParent, item1, item2) {
      this.keyParentActive = keyParent
      this.keyChild1Active = item1.key
      this.keyChild2Active = item2.key
      const form = {
        keyParent,
        keyChild1: item1.key,
        keyChild2: item2.key,
        dataItem: item2.data,
      }
      this.$emit('dataMenu', form)
    },
    formatData(key) {
      if (key === 'CHOXULY') {
        this.dataShow = []
        // this.dataApi.map(item => {
        //   if(item.trangthai === '')
        // })
      } else if (key === 'DANGXULY') {
        console.log(12)
      } else if (key === 'DAXULY') {
        console.log(12)
      } else if (key === 'QUAHANXULY') {
        console.log(12)
      } else if (key === 'VPUBNDTINH') {
        console.log(12)
      } else if (key === 'SOBANNGANH') {
        console.log(12)
      } else if (key === 'DIAPHUONG') {
        console.log(12)
      } else if (key === 'TONGQUAN') {
        console.log(1212)
      }
    },
  },
}
</script>

<style lang="scss">
.sibar-y-kien-nguoidan {
  .baocao-task-list {
    li {
      list-style: none;
      font-size: 14px;
      .name-parent {
        font-weight: 600;
      }
    }
    .item {
      padding: 8px 15px;
      cursor: pointer;
      font-size: 16px;
      .icon {
        width: 25px;
      }
      &.active {
        color: #5a8dee;
        border-left: 2px solid #5a8dee;
      }
    }
    .child-report {
      .item {
        padding-left: 0;
        .name {
          width: 100%;
        }
        .count-item {
          width: 13%;
          .count {
            background: #e6eefc;
            width: 25px;
            height: 25px;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 1px solid #e6eefc;
            border-radius: 2px;
            font-size: 12px;
            color: #5a8dee;
          }
        }
        &.active {
          border-left: 0;
          svg {
            color: #5a8dee;
          }
          .count-item {
            .count {
              background: #5a8dee;
              color: #fff;
            }
          }
        }
      }
    }
  }
  .sidebar-menu-list {
    position: relative;
    padding: 10px 0;
    height: calc(100% - 50px) !important;
  }
  .btn-open-hop-phan{
    button{
      width: 60%
    }
  }
}
</style>
