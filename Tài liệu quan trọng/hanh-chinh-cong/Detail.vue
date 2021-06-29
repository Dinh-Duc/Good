<template>
  <div>
    <div class="row">
      <div class="col-md-6">
        <b-card class="box-hcc box-border-ml-left">
          <div class="progress-list progress-list-hcc">
            <div class="mb-1 text-center">
              <span class="title-progress-hcc">{{
                dataDetai.box_progress.title
              }}</span>
            </div>
            <b-progress
              v-if="dataDetai.box_progress"
              class="mt-2"
              :max="dataDetai.box_progress.max_progress"
            >
              <b-progress-bar
                v-for="(item, index) in dataDetai.box_progress.progress"
                :key="index"
                :class="`${item.key}`"
                :value="item.value"
              >
                <span class="cursor-pointer nut-progress-bar">
                  {{ item.value }}</span>
              </b-progress-bar>
            </b-progress>
            <b-row class="mx-0 my-2">
              <b-col
                v-for="(item, index) in dataDetai.box_progress.progress"
                :key="index"
                xl="3"
                lg="12"
                sm="12"
                class="px-0 d-flex -align-items-center"
              >
                <div :class="`label-progress-hcc ${item.key}`" />
                <div>{{ item.title }}</div>
              </b-col>
            </b-row>
            <div
              class="border-top progress-status-hc d-flex align-items-center justify-content-center"
            >
              <div
                v-for="(item, index) in dataDetai.box_progress.description"
                :key="index"
                class="status-hc mr-2 py-1"
              >
                <div class="cursor-pointer">
                  <span :class="`${item.key}`">{{ item.value }} </span><span>{{ item.title }}</span>
                </div>
              </div>
            </div>
          </div>
        </b-card>
      </div>
      <div class="col-md-6">
        <b-card class="box-hcc box-hs box-border-ml-left">
          <div class="progress-list">
            <div
              v-if="Object.keys(dataDetai.box_thongke).length > 0"
              class="mb-1 text-center"
            >
              <span class="title-progress-hcc">{{
                dataDetai.box_thongke.title
              }}</span>
            </div>
            <div v-if="Object.keys(dataDetai.box_thongke).length > 0">
              <b-row
                v-for="(item, index) in dataDetai.box_thongke.data"
                :key="index"
                class="mb-2"
              >
                <b-col
                  xl="4"
                  sm="6"
                >
                  {{ item.title }}
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
          </div>
        </b-card>
      </div>
      <div class="col-md-12">
        <BoxTable :data="dataDetai.box_table" />
      </div>
    </div>
  </div>
</template>

<script>
// eslint-disable-next-line import/extensions
import BoxTable from './boxTable'

export default {
  components: {
    BoxTable,
  },
  props: {
    dataItem: {
      type: Object,
      default() {
        return {}
      },
    },
  },
  data() {
    return {}
  },
  computed: {
    dataDetai() {
      return this.dataItem
    },
  },
  watch: {
    dataItem(val) {
      console.log('detail', val)
    },
  },
  created() {},
  methods: {
  },
}
</script>
<style lang="scss">
.progress-list-hcc {
  .DAXULY {
    background-color: rgb(40, 167, 69);
  }
  .CHOXULY {
    background-color: rgb(255, 193, 7);
  }
  .DANGXULY {
    background-color: rgb(23, 162, 184);
  }
  .QUAHAN {
    color:rgb(255, 41, 41);
  }
  .DENHAN {
    color: rgb(6, 194, 112);
  }
  .TRONGHAN {
    color: rgb(153, 30, 249);
  }
}
</style>
