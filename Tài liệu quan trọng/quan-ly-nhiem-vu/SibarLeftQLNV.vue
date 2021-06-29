<template>
  <div class="sidebar-left">
    <div class="sidebar">
      <div class="sidebar-content todo-sidebar">
        <div class="todo-app-menu sibar-quan-ly-nhiem-vu">
          <vue-perfect-scrollbar
            :settings="perfectScrollbarSettings"
            class="sidebar-menu-list scroll-area py-2"
          >
            <ul class="baocao-task-list list-y-kien-nguoi-dan p-0 m-0">
              <li v-for="(item, key) in listNv" :key="key" class="baocao-item">
                <div
                  :class="{
                    'item d-flex align-items-center': true,
                    active: item.key == idActive,
                  }"
                  @click="showChildReport(item)"
                >
                  <div v-if="item.icon" class="icon">
                    <feather-icon class="mr-1" :icon="item.icon" size="14" />
                  </div>
                  <div class="name-parent">
                    {{ item.title }}
                  </div>
                  <div
                    v-if="item.count > 0"
                    class="count-item d-flex justify-content-end"
                  >
                    <label class="count">
                      {{ item.count }}
                    </label>
                  </div>
                </div>
                <div class="child-report">
                  <ul
                    v-if="item.childs && item.childs.length > 0"
                    class="mt-0 pl-2"
                  >
                    <li v-for="(item1, key1) in item.childs" :key="key1">
                      <div
                        :class="{
                          'item d-flex align-items-center': true,
                          active: item1.key == keyActive,
                        }"
                        @click="eventChild(item.key, item1)"
                      >
                        <div v-if="item1.icon" class="icon">
                          <feather-icon
                            class="mr-1"
                            :icon="item1.icon"
                            size="14"
                          />
                        </div>
                        <div class="name">
                          {{ item1.title }}
                        </div>
                        <div class="count-item d-flex justify-content-end">
                          <label class="count">
                            {{ item1.count }}
                          </label>
                        </div>
                      </div>
                      <div
                        v-if="
                          item1.childs &&
                          item1.childs.length > 0 &&
                          item1.key == keyActive
                        "
                        class="child-lv-3"
                      >
                        <ul class="mt-0">
                          <li v-for="(item2, key2) in item1.childs" :key="key2">
                            <div
                              :class="{
                                'item d-flex align-items-center': true,
                                active: item2.key == idSubActive2,
                              }"
                              @click="eventChild2(item.key, item1, item2)"
                            >
                              <div class="name">
                                {{ item2.title }}
                              </div>
                              <div
                                class="count-item d-flex justify-content-end"
                              >
                                <label class="count">
                                  {{ item2.count }}
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
            <b-button variant="primary" @click="actionGenerateUrl()">
              Xử lý nhiệm vụ
            </b-button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import VuePerfectScrollbar from "vue-perfect-scrollbar";
import { generateUrl } from "@/api/quan-ly-nhiem-vu";
import datajson from "./data.json";

export default {
  components: {
    VuePerfectScrollbar,
  },
  data() {
    return {
      perfectScrollbarSettings: {
        maxScrollbarLength: 60,
      },
      // listReport: [
      //   {
      //     title: 'Tổng quan',
      //     key: 'TONGQUAN',
      //     count: 52,
      //     childs: [],
      //     icon: '',
      //   },
      //   {
      //     title: 'Nhiệm vụ của tôi',
      //     key: 'NHIEMVUCUATOI',
      //     count: 15,
      //     childs: [],
      //     icon: '',
      //   },
      //   {
      //     title: 'Nhiệm vụ đơn vị',
      //     key: 'NHIEMVUDONVI',
      //     count: 25,
      //     childs: [],
      //     icon: '',
      //   },
      //   {
      //     title: 'Mức độ',
      //     key: 'MUCDONV',
      //     count: 0,
      //     childs: [
      //       {
      //         title: 'Gấp',
      //         key: 'GAP',
      //         count: 20,
      //         childs: [],
      //         icon: 'LayersIcon',
      //       },
      //       {
      //         title: 'Quan trọng',
      //         key: 'QUANTRONG',
      //         count: 15,
      //         childs: [],
      //         icon: 'LayersIcon',
      //       },
      //       {
      //         title: 'Bình thường',
      //         key: 'BINHTHUONG',
      //         count: 27,
      //         childs: [],
      //         icon: 'LayersIcon',
      //       },
      //     ],
      //     icon: '',
      //   },
      //   {
      //     title: 'Loại nhiệm vụ',
      //     key: 'LOAINHIEMVU',
      //     count: 0,
      //     childs: [
      //       {
      //         title: 'Nhiệm vụ chính phủ',
      //         key: 'NHIEMVUCHINHPHU',
      //         count: 11,
      //         childs: [],
      //         icon: 'LayersIcon',
      //       },
      //       {
      //         title: 'Hội đồng nhân dân',
      //         key: 'HOIDONGNHANDAN',
      //         count: 8,
      //         childs: [],
      //         icon: 'LayersIcon',
      //       },
      //       {
      //         title: 'Tỉnh ủy',
      //         key: 'TINHUY',
      //         count: 32,
      //         childs: [],
      //         icon: 'LayersIcon',
      //       },
      //     ],
      //     icon: '',
      //     dataApi: [],
      //   },
      //   {
      //     title: 'Đơn vị thực hiện',
      //     key: 'DONVITHUCHIEN',
      //     count: 0,
      //     childs: [
      //       {
      //         title: 'Tỉnh ủy',
      //         key: 'DVTINHUY',
      //         count: 1,
      //         childs: [],
      //         icon: 'LayersIcon',
      //       },
      //       {
      //         title: 'Ủy ban nhân dân',
      //         key: 'DVUYBANNHANDAN',
      //         count: 1,
      //         childs: [],
      //         icon: 'LayersIcon',
      //       },
      //       {
      //         title: 'Hội đồng nhân dân',
      //         key: 'DVHOIDONGNHANDAN',
      //         count: 1,
      //         childs: [],
      //         icon: 'LayersIcon',
      //       },
      //       {
      //         title: 'Sở GTVT',
      //         key: 'DVSGTVT',
      //         count: 1,
      //         childs: [],
      //         icon: 'LayersIcon',
      //       },
      //     ],
      //     icon: '',
      //     dataApi: [],
      //   },
      // ],
      idActive: "TONGQUAN",
      keyActive: "",
      listNv: datajson,
      idSubActive2: "",
    };
  },
  created() {
    const form = {
      key: "TONGQUAN",
      keyChild: "",
    };
    this.$eventBus.$emit("quan-ly-nhiem-vu", form);

    // COMMON_POST2('http://btnmt-qlnvbe.chinhquyendientu.vn/api/qlnv/nhiem-vu/dem-loai-nhiem-vu/donvi', {})
    // .then(res => {
    //   console.log(123, res)
    // })
  },
  methods: {
    actionGenerateUrl() {
      generateUrl()
        .then((data) => {
          if (data.statusCode === 200 && data.succeeded) {
            window.open(`${data.data.url}/redirect?otp=${data.data.key}`);
          }
        })
        .catch((err) => {
          console.log(err);
        });
    },
    openUrl(url) {
      window.open(url, "_blank");
    },
    showChildReport(item) {
      this.idActive = item.key;
      if (item.childs && item.childs.length > 0) {
        // this.keyActive = item.childs[0].key
        // const form = {
        //   key: item.key,
        //   keyChild: item.childs[0].key,
        //   dataApi: item.childs[0].dataApi,
        // }
        // this.$eventBus.$emit('quan-ly-nhiem-vu', form)
        this.eventChild(item.key, item.childs[0]);
      } else {
        this.keyActive = "";
        const form = {
          key: item.key,
          keyChild: "",
          dataApi: item.dataApi,
        };
        this.$eventBus.$emit("quan-ly-nhiem-vu", form);
      }
    },
    eventChild(keyParent, item) {
      this.idActive = keyParent;
      this.keyActive = item.key;
      if (item.childs && item.childs.length > 0) {
        this.idSubActive2 = item.childs[0].key;
        const form = {
          key: keyParent,
          keyChild: item.key,
          dataApi: item.childs[0].dataApi,
        };
        this.$eventBus.$emit("quan-ly-nhiem-vu", form);
      } else {
        this.idSubActive2 = "";
        const form = {
          key: keyParent,
          keyChild: item.key,
          dataApi: item.dataApi,
        };
        this.$eventBus.$emit("quan-ly-nhiem-vu", form);
      }
    },
    eventChild2(keyParent, item1, item2) {
      this.idActive = keyParent;
      this.keyActive = item1.key;
      this.idSubActive2 = item2.key;
      const form = {
        key_parent: keyParent,
        key_child: item1.key,
        dataApi: item2.dataApi,
      };
      this.$eventBus.$emit("quan-ly-nhiem-vu", form);
    },
  },
};
</script>

<style lang="scss">
.sibar-quan-ly-nhiem-vu {
  .baocao-task-list {
    li {
      list-style: none;
      font-size: 14px;
      .name-parent {
        font-weight: 600;
        width: 100%;
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
        .count-item {
          .count {
            background: #5a8dee;
            color: #fff;
          }
        }
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
  .btn-open-hop-phan {
    button {
      width: 60%;
    }
  }
}
</style>
