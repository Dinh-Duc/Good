<template>
  <div>
    <div class="row">
      <div class="col-md-6">
        <b-card class="box-hcc box-border-ml-left">
          <div class="progress-list">
            <div class="mb-1 text-center">
              <span class="title-progress-hcc">Ý kiến người dân</span>
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
                xl="3"
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
                  <span :style="`color: ${item.color}`">{{ item.value }} </span><span>{{ item.name }}</span>
                </div>
              </div>
            </div>
          </div>
        </b-card>
      </div>
      <div class="col-md-6">
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
      </div>
      <div class="col-md-12">
        <BoxTable :data="dataTable" />
      </div>
    </div>
  </div>
</template>

<script>
// eslint-disable-next-line import/extensions
import BoxTable from './BoxTable'

export default {
  components: {
    BoxTable,
  },
  data() {
    return {
      progress: 100,
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
          name: 'Vụ Địa chất',
          value: 25,
          max: 100,
        },
        {
          name: 'Vụ Khoáng sản',
          value: 12,
          max: 80,
        },
        {
          name: 'Vụ Chính sách và Pháp chế',
          value: 18,
          max: 85,
        },
        {
          name: 'Vụ Khoa học, Công nghệ và Hợp tác quốc tế',
          value: 54,
          max: 60,
        },
        {
          name: 'Vụ Kế hoạch - Tài chính',
          value: 68,
          max: 100,
        },
        {
          name: 'Vụ Tổ chức cán bộ',
          value: 99,
          max: 150,
        },
        {
          name: 'Văn phòng Tổng cục',
          value: 10,
          max: 100,
        },
        {
          name: 'Cục Kinh tế Địa chất và Khoáng sản',
          value: 20,
          max: 100,
        },
        {
          name: 'Cục Kiểm soát hoạt động khoáng sản miền Bắc',
          value: 30,
          max: 100,
        },
        {
          name: 'Cục Kiểm soát hoạt động khoáng sản miền Trung',
          value: 40,
          max: 100,
        },
        {
          name: 'Cục Kiểm soát hoạt động khoáng sản miền Nam',
          value: 50,
          max: 100,
        },
        {
          name: 'Liên đoàn Bản đồ Địa chất miền Bắc',
          value: 70,
          max: 100,
        },
        {
          name: 'Liên đoàn Bản đồ Địa chất miền Nam',
          value: 50,
          max: 100,
        },
        {
          name: 'Liên đoàn Địa chất Đông Bắc',
          value: 50,
          max: 100,
        },
        {
          name: 'Liên đoàn Địa chất Tây Bắc',
          value: 80,
          max: 100,
        },
        {
          name: 'Liên đoàn Địa chất Bắc Trung Bộ',
          value: 70,
          max: 100,
        },
        {
          name: 'Liên đoàn Địa chất Trung Trung Bộ',
          value: 50,
          max: 100,
        },
        {
          name: 'Liên đoàn Địa chất Xạ - Hiếm',
          value: 40,
          max: 100,
        },
        {
          name: 'Liên đoàn Vật lý Địa chất',
          value: 45,
          max: 100,
        },
        {
          name: 'Liên đoàn INTERGEO',
          value: 34,
          max: 100,
        },
        {
          name: 'Liên đoàn Địa chất và Khoáng sản biển',
          value: 10,
          max: 100,
        },
        {
          name: 'Trung tâm Kiểm định địa chất',
          value: 5,
          max: 100,
        },
        {
          name: 'Trung tâm Phân tích thí nghiệm địa chất',
          value: 34,
          max: 100,
        },
        {
          name: 'Trung tâm Thông tin, Lưu trữ và Tạp chí địa chất',
          value: 3,
          max: 100,
        },
        {
          name: 'Bảo tàng Địa chất',
          value: 8,
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
              'Tôi muốn xem quy hoạch bản đồ địa chất vùng Tây Bắc giai đoạn 2021 thì xem ở đâu',
            COQUANXULY: ' Tổng cục Địa chất và khoáng sản Việt Nam',
            NGAYTIEPNHAN: '05/05/2021',
            NGAYXULY: '07/05/2021',
            TRANGTHAI: 'Chờ xử lý',
          },
          {
            NOIDUNGPHANANH:
              'Tôi muốn mua đất tại xã Phú Hữu, số tờ bản đồ là 30, thửa 420. Tôi muốn nhờ coi dùm khu đất này có bị quy hoạch gì hay không',
            COQUANXULY: 'Tổng cục Quản lý đất đai',
            NGAYTIEPNHAN: '05/05/2021',
            NGAYXULY: '07/05/2021',
            TRANGTHAI: 'Chờ xử lý',
          },
          {
            NOIDUNGPHANANH:
              'Tôi muốn xem quy hoạch bản đồ địa chất vùng Tây Bắc giai đoạn 2021 thì xem ở đâu',
            COQUANXULY: ' Tổng cục Địa chất và khoáng sản Việt Nam',
            NGAYTIEPNHAN: '05/05/2021',
            NGAYXULY: '07/05/2021',
            TRANGTHAI: 'Chờ xử lý',
          },
        ],
      },
    }
  },
}
</script>
