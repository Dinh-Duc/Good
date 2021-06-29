<template>
  <div>
    <div class="row">
      <div class="col-md-6">
        <b-card class="box-hcc box-border-ml-left">
          <div class="progress-list progress-list-qlnv">
            <div class="mb-1 text-center">
              <span class="title-progress-hcc">Nhiệm vụ</span>
            </div>
            <b-progress
              v-if="dataItem.nhiemvu.data_nv"
              class="mt-2"
              :max="dataItem.nhiemvu.max_process"
            >
              <b-progress-bar
                v-for="(item, index) in dataItem.nhiemvu.data_nv"
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
                v-for="(item, index) in dataItem.nhiemvu.data_nv"
                :key="index"
                xl="3"
                lg="12"
                sm="12"
                class="px-0 d-flex -align-items-center"
              >
                <div :class="`label-progress-hcc ${item.key}`" />
                <div>{{ item.text }}</div>
              </b-col>
            </b-row>
            <div
              class="border-top progress-status-hc d-flex align-items-center justify-content-center"
            >
              <div
                v-for="(item, index) in dataItem.nhiemvu.status"
                :key="index"
                class="status-hc mr-2 py-1"
              >
                <div class="cursor-pointer">
                  <span :class="`${item.key}`">{{ item.value }} </span><span>{{ item.name }}</span>
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
              v-if="Object.keys(dataItem.chartData).length == 0"
              class="mb-1 text-center"
            >
              <span
                class="title-progress-hcc"
              >Thống kê nhiệm vụ chưa hoàn thành theo đơn vị xử lý</span>
            </div>
            <div v-if="Object.keys(dataItem.chartData).length == 0">
              <b-row
                v-for="(item, index) in dataItem.thongke"
                :key="index"
                class="mb-2"
                @click="changeDataTableBySo(dataItem)"
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
            <div v-else>
              <BoxChart :data="dataItem.chartData" />
            </div>
          </div>
        </b-card>
      </div>
      <div class="col-md-12">
        <BoxTable :data="dataItem.data_table" />
      </div>
    </div>
  </div>
</template>

<script>
// eslint-disable-next-line import/extensions
import BoxTable from './BoxTable'
// eslint-disable-next-line import/extensions
import BoxChart from './BoxChart'

export default {
  components: {
    BoxTable,
    BoxChart,
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
    return {
      progress: 68,
      dataProgress: [
        {
          value: 10,
          color: '#FFC206',
          status: 'Chờ vào sổ',
        },
        {
          value: 20,
          color: '#FF4D01',
          status: 'Chờ xử lý',
        },
        {
          value: 30,
          color: '#5396FF',
          status: 'Chờ phân xử lý',
        },
        {
          value: 40,
          color: '#66D8FF',
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
      dataHoSo: [
        {
          name: 'Sở Tài chính',
          value: 25,
          max: 100,
        },
        {
          name: 'Sở Kế hoạch và Đầu tư',
          value: 12,
          max: 100,
        },
      ],
      dataTable: {
        fields: [
          {
            key: 'STT',
            label: 'STT',
            sortable: false,
          },
          {
            key: 'NOIDUNGPHANANH',
            label: 'NỘI DUNG PHẢN ÁNH',
            sortable: false,
          },
          {
            key: 'COQUANXULY',
            label: 'CƠ QUAN XỬ LÝ',
            sortable: false,
          },
          {
            key: 'NGAYTIEPNHAN',
            label: 'NGÀY TIẾP NHẬN',
            sortable: false,
          },
          {
            key: 'NGAYXULY',
            label: 'Ngày XỬ LÝ',
            sortable: false,
          },
          {
            key: 'TRANGTHAI',
            label: 'TRẠNG THÁI',
            sortable: false,
          },
        ],
        items: [
          {
            NOIDUNGPHANANH:
              'Tôi muốn mua đất tại xã An Khánh, số tờ bảnđồ là 30, thửa 420. Tôi muốn nhờ coi dùm khu đất này có bị quy hoạch gì hay không',
            COQUANXULY: 'Sở Tài nguyên và Môi trường',
            NGAYTIEPNHAN: '05/05/2021',
            NGAYXULY: '07/05/2021',
            TRANGTHAI: 'Chờ xử lý',
          },
          {
            NOIDUNGPHANANH:
              'Tôi muốn mua đất tại xã An Khánh, số tờ bản đồ là 30, thửa 420. Tôi muốn nhờ coi dùm khu đất này có bị quy hoạch gì hay không',
            COQUANXULY: 'Sở Tài nguyên và Môi trường',
            NGAYTIEPNHAN: '05/05/2021',
            NGAYXULY: '07/05/2021',
            TRANGTHAI: 'Chờ xử lý',
          },
          {
            NOIDUNGPHANANH:
              'Tôi muốn mua đất tại xã An Khánh, số tờ bảnđồ là 30, thửa 420. Tôi muốn nhờ coi dùm khu đất này có bị quy hoạch gì hay không',
            COQUANXULY: 'Sở Tài nguyên và Môi trường',
            NGAYTIEPNHAN: '05/05/2021',
            NGAYXULY: '07/05/2021',
            TRANGTHAI: 'Chờ xử lý',
          },
        ],
      },
    }
  },
  methods: {
    changeDataTableBySo(data) {
      // eslint-disable-next-line no-param-reassign
      data.data_table = {
        fields: [
          {
            key: 'SONHIEMVU',
            label: 'Số nhiệm vụ',
            sortable: false,
          },
          {
            key: 'NOIDUNG',
            label: 'Nội dung',
            sortable: false,
          },
          {
            key: 'DVTHUCHIEN',
            label: 'Đơn vị thực hiện',
            sortable: false,
          },
          {
            key: 'HANXULY',
            label: 'Hạn xử lý',
            sortable: false,
          },
          {
            key: 'LOAINHIEMVU',
            label: 'Loại nhiệm vụ',
            sortable: false,
          },
          {
            key: 'TRANGTHAIXL',
            label: 'Trạng thái xử lý',
            sortable: false,
          },
          {
            key: 'TRANGTHAI',
            label: 'Trạng thái',
            sortable: false,
          },
          {
            key: 'TINHCHAT',
            label: 'Tính chất',
            sortable: false,
          },
        ],
        items: [
          {
            SONHIEMVU: 'NVDV16',
            NOIDUNG: 'Tổ chức thi chọn học sinh giỏi quốc gia, quốc tế',
            DVTHUCHIEN: 'Sở Tài chính',
            HANXULY: '20/05/2021',
            LOAINHIEMVU: 'Nhiệm vụ địa phương',
            TRANGTHAIXL: 'Trong hạn',
            TRANGTHAI: 'Đang xử lý',
            TINHCHAT: 'Bình thường',
          },
          {
            SONHIEMVU: 'NVDV16',
            NOIDUNG: 'Tổ chức thi chọn học sinh giỏi quốc gia, quốc tế',
            DVTHUCHIEN: 'Sở Tài chính',
            HANXULY: '20/05/2021',
            LOAINHIEMVU: 'Nhiệm vụ địa phương',
            TRANGTHAIXL: 'Quá hạn',
            TRANGTHAI: 'Chưa xử lý',
            TINHCHAT: 'Bình thường',
          },
        ],
      }
      // eslint-disable-next-line no-param-reassign
      data.thongke = [
        {
          name: 'Lãnh đạo sở',
          value: 3,
          max: 5,
        },
        {
          name: 'Văn phòng',
          value: 6,
          max: 8,
        },
        {
          name: 'Thanh tra sở',
          value: 2,
          max: 3,
        },
        {
          name: 'Phòng ngân sách',
          value: 4,
          max: 5,
        },
        {
          name: 'Phòng tài chính HCNS',
          value: 13,
          max: 15,
        },
        {
          name: 'Phòng giá - công sản',
          value: 2,
          max: 4,
        },
        {
          name: 'Phòng đầu tư',
          value: 2,
          max: 5,
        },
      ]
    },
  },
}
</script>
<style lang="scss">
.progress-list-qlnv {
  .CHUATHUCHIEN {
    background-color: #796eef;
  }
  .DANGTHUCHIEN {
    background-color: #ff9f43;
  }
  .DAHOANTHANH {
    background-color: #51cd89;
  }
  .QUAHAN {
    color: #796eef;
  }
  .DENHAN {
    color: #ff9f43;
  }
  .TRONGHAN {
    color: #51cd89;
  }
}
</style>
