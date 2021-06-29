<template>
  <div class="w-100 h-100">
    <div class="w-100 h-100 p-2 iframe-bc">
      <!-- https://app.powerbi.com/view?r=eyJrIjoiZGE5ODgwYjEtYzNmZi00NmE4LWEwNjUtYWYzYTc0NGI0ZjFlIiwidCI6IjY4ZTQxNzUxLTgwZDMtNDE4My1hZjdiLWE1YzQyMTJiZGZlNSIsImMiOjEwfQ%3D%3D -->
      <iframe
        class="inner iframeAP"
        src="https://app.powerbi.com/view?r=eyJrIjoiYzQxNzU1M2ItOTQ1Ni00NTQzLTg3MzgtYmMyY2FkOTcxNzJmIiwidCI6IjY4ZTQxNzUxLTgwZDMtNDE4My1hZjdiLWE1YzQyMTJiZGZlNSIsImMiOjEwfQ%3D%3D"
        frameborder="0"
        width="100%"
        height="100%"
        style="border-radius: 5px"
      />
    </div>
    <div class="dashboard-hcc hide hidden">
      <b class="title-hcc">Lĩnh vực</b>

      <!-- Table -->
      <div class="elm-data-dashboard">
        <div class="table-data">
          <boxTable :data="boxTable" />
        </div>
      </div>

      <!-- Chart 1 -->
      <div class="elm-data-dashboard">
        <!-- Theo lĩnh vực -->
        <b-col
          cols="6"
          style="float: left;"
        >
          <div class="data-chart-elm">
            <b class="title-box-chart">Đánh giá mức độ hài lòng theo lĩnh vực</b>
            <div class="chart-content">
              <ApexCharts
                type="bar"
                height="420"
                :options="linhvuc_chartOptions"
                :series="linhvuc_series"
              />
            </div>
          </div>
        </b-col>

        <!-- Theo địa phương -->
        <b-col
          cols="6"
          style="float: left;"
        >
          <div class="data-chart-elm">
            <b
              class="title-box-chart"
            >Đánh giá mức độ hài lòng theo địa phương</b>
            <div class="chart-content">
              <ApexCharts
                type="bar"
                height="420"
                :options="diaPhuong_chartOptions"
                :series="diaPhuong_series"
              />
            </div>
          </div>
        </b-col>
      </div>

      <!-- Chart 2 -->
      <div class="elm-data-dashboard">
        <b-col
          cols="6"
          style="float: left;"
        >
          <!-- Progress -->
          <div class="data-chart-elm">
            <div class="elm-chart-2">
              <b class="title-box-chart">Số hồ sơ tiếp nhận (17.234)</b>
              <div class="progress-data">
                <div class="prt-progress">
                  <b-progress
                    show-progress
                    :max="100"
                  >
                    <b-progress-bar
                      style="background: #796EEF"
                      :value="120"
                    />
                    <b-progress-bar
                      style="background: #FF9F43"
                      :value="56"
                    />
                    <b-progress-bar
                      style="background: #00CFE8"
                      :value="17"
                    />
                    <b-progress-bar
                      style="background: #51CD89"
                      :value="17"
                    />
                  </b-progress>
                </div>
                <div class="note-progress">
                  <div class="note-elm-3">
                    <div
                      class="elm-square"
                      style="background: #796EEF"
                    />
                    <span>Chờ vào sổ</span>
                  </div>
                  <div class="note-elm-3">
                    <div
                      class="elm-square"
                      style="background: #FF9F43"
                    />
                    <span>Chờ phân xử lý</span>
                  </div>
                  <div class="note-elm-3">
                    <div
                      class="elm-square"
                      style="background: #00CFE8"
                    />
                    <span>Chờ xử lý</span>
                  </div>
                  <div class="note-elm-3">
                    <div
                      class="elm-square"
                      style="background: #51CD89"
                    />
                    <span>Đang xử lý</span>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Chart line -->
          <div class="data-chart-elm elm-margin-custom">
            <div class="elm-chart-2">
              <b class="title-box-chart">Tình trạng xử lý qua các năm</b>
              <div class="chart-content">
                <ApexCharts
                  type="line"
                  height="233"
                  :options="line_chartOptions"
                  :series="line_series"
                />
              </div>
            </div>
          </div>
        </b-col>
        <b-col
          cols="6"
          style="float: left;"
        >
          <div class="data-chart-elm">
            <b
              class="title-box-chart"
            >Tổng số hồ sơ quá hạn phân theo đơn vị xử lý (2021)</b>
            <div class="chart-content">
              <ApexCharts
                type="bar"
                height="420"
                :options="tongHS_chartOptions"
                :series="tongHS_series"
              />
            </div>
          </div>
        </b-col>
      </div>
    </div>
  </div>
</template>
<script>
import ApexCharts from 'vue-apexcharts'
import boxTable from './boxTable.vue'

export default {
  components: {
    ApexCharts,
    boxTable,
  },
  data() {
    return {
      boxTable: {
        fields: [
          {
            key: 'linhVuc',
            label: 'LĨNH VỰC',
            sortable: true,
          },
          {
            key: 'soHoSo',
            label: 'SỐ HỒ SƠ',
            sortable: false,
          },
          {
            key: 'chuHoSo',
            label: 'QUÁ HẠN XỬ LÝ',
            sortable: true,
          },
          {
            key: 'hoanThanh',
            label: 'HOÀN THÀNH',
            sortable: true,
          },
          {
            key: 'hoanThanhDungHan',
            label: 'HOÀN THÀNH ĐÚNG HẠN',
            sortable: true,
          },
        ],
        items: [
          {
            linhVuc: 'Cải cách hành chính',
            soHoSo: '944',
            chuHoSo: '57.14%',
            hoanThanh: '20.00%',
            hoanThanhDungHan: '42.00%',
          },
          {
            linhVuc: 'Chính quyền địa phương',
            soHoSo: '1520',
            chuHoSo: '51.23%',
            hoanThanh: '60.00%',
            hoanThanhDungHan: '26.00%',
          },
          {
            linhVuc: 'Công chức, viên chức',
            soHoSo: '1630',
            chuHoSo: '62.00%',
            hoanThanh: '84.00%',
            hoanThanhDungHan: '46.00%',
          },
          {
            linhVuc: 'Công tác Thanh niên',
            soHoSo: '2000',
            chuHoSo: '53.00%',
            hoanThanh: '68.00%',
            hoanThanhDungHan: '42.08%',
          },
          {
            linhVuc: 'Đào tạo, bồi dưỡng cán bộ công chức',
            soHoSo: '1900',
            chuHoSo: '52.21%',
            hoanThanh: '63.00%',
            hoanThanhDungHan: '68.30%',
          },
          {
            linhVuc: 'Hợp tác quốc tế',
            soHoSo: '900',
            chuHoSo: '56.36%',
            hoanThanh: '60.00%',
            hoanThanhDungHan: '52.00%',
          },
          {
            linhVuc: 'Kế hoạch tài chính',
            soHoSo: '1500',
            chuHoSo: '32.00%',
            hoanThanh: '80.00%',
            hoanThanhDungHan: '36.00%',
          },
          {
            linhVuc: 'Pháp chế',
            soHoSo: '2200',
            chuHoSo: '43.00%',
            hoanThanh: '67.00%',
            hoanThanhDungHan: '60.00%',
          },
          {
            linhVuc: 'Thanh tra',
            soHoSo: '1690',
            chuHoSo: '30.00%',
            hoanThanh: '76.00%',
            hoanThanhDungHan: '69.00%',
          },
          {
            linhVuc: 'Thi đua - Khen thưởng',
            soHoSo: '1420',
            chuHoSo: '36.00%',
            hoanThanh: '63.00%',
            hoanThanhDungHan: '43.00%',
          },
          {
            linhVuc: 'Tiền lương',
            soHoSo: '1500',
            chuHoSo: '36.40%',
            hoanThanh: '63.00%',
            hoanThanhDungHan: '45.00%',
          },
          {
            linhVuc: 'Tổ chức biên chế',
            soHoSo: '568',
            chuHoSo: '42.00%',
            hoanThanh: '62.00%',
            hoanThanhDungHan: '25.00%',
          },
          {
            linhVuc: 'Tổ chức cán bộ',
            soHoSo: '1680',
            chuHoSo: '36.00%',
            hoanThanh: '60.00%',
            hoanThanhDungHan: '53.00%',
          },
          {
            linhVuc: 'Tổ chức phi chính phủ',
            soHoSo: '2160',
            chuHoSo: '25.00%',
            hoanThanh: '65.00%',
            hoanThanhDungHan: '36.00%',
          },
          {
            linhVuc: 'Tôn giáo, tín ngưỡng',
            soHoSo: '2300',
            chuHoSo: '45.00%',
            hoanThanh: '68.00%',
            hoanThanhDungHan: '53.00%',
          },
          {
            linhVuc: 'Tổng hợp',
            soHoSo: '690',
            chuHoSo: '20.00%',
            hoanThanh: '70.00%',
            hoanThanhDungHan: '65.00%',
          },
          {
            linhVuc: 'Văn thư lưu trữ',
            soHoSo: '860',
            chuHoSo: '56.00%',
            hoanThanh: '79.00%',
            hoanThanhDungHan: '50.00%',
          },
        ],
      },

      /* Chart lĩnh vực */
      linhvuc_chartOptions: {
        chart: {
          type: 'bar',
          height: 385,
          stacked: true,
          toolbar: false,
        },
        plotOptions: {
          bar: {
            horizontal: true,
          },
        },
        stroke: {
          width: 1,
          colors: ['#fff'],
        },
        xaxis: {
          categories: [
            'Cải cách hành chính',
            'Chính quyền địa phương',
            'Công chức, viên chức',
            'Công tác Thanh niên',
            'Đào tạo, bồi dưỡng cán bộ công chức',
            'Hợp tác quốc tế',
            'Kế hoạch tài chính',
            'Pháp chế',
          ],
          labels: {
            style: {
              colors: ['#40566F'],
              fontSize: '14px',
              fontWeight: 400,
            },
          },
        },
        yaxis: {
          title: {
            text: undefined,
          },
        },
        fill: {
          opacity: 1,
        },
        colors: ['#28C76F', '#FAAF40'],
        grid: {
          show: true,
          xaxis: {
            lines: {
              show: true,
            },
          },
          yaxis: {
            lines: {
              show: false,
            },
          },
          strokeDashArray: 5,
        },
      },
      linhvuc_series: [
        {
          name: 'Hài lòng',
          data: [4000, 5282, 1363, 3894, 2569, 2733, 6622, 2229],
        },
        {
          name: 'Chưa hài lòng',
          data: [5354, 1231, 4656, 6787, 6789, 792, 5667, 2329],
        },
      ],

      /* Chart địa phương */
      diaPhuong_chartOptions: {
        chart: {
          type: 'bar',
          height: 385,
          stacked: true,
          toolbar: false,
        },
        plotOptions: {
          bar: {
            horizontal: true,
          },
        },
        stroke: {
          width: 1,
          colors: ['#fff'],
        },
        xaxis: {
          categories: [
            'TP Hà Nội',
            'TP HCM',
            'Tỉnh Đồng Nai',
            'Tỉnh Bắc Ninh',
            'Tỉnh Bắc Giang',
            'Tỉnh Hà Tĩnh',
            'TP Đà Nẵng',
            'Tỉnh Bình Dương',
            'Tỉnh Kiên Giang',
          ],
          labels: {
            style: {
              colors: ['#40566F'],
              fontSize: '14px',
              fontWeight: 400,
            },
          },
        },
        yaxis: {
          title: {
            text: undefined,
          },
        },
        fill: {
          opacity: 1,
        },
        colors: ['#28C76F', '#FAAF40'],
        grid: {
          show: true,
          xaxis: {
            lines: {
              show: true,
            },
          },
          yaxis: {
            lines: {
              show: false,
            },
          },
          strokeDashArray: 5,
        },
      },
      diaPhuong_series: [
        {
          name: 'Hài lòng',
          data: [1564, 4182, 6663, 1894, 2569, 1733, 2622, 3229],
        },
        {
          name: 'Chưa hài lòng',
          data: [1231, 2423, 987, 1645, 2341, 2123, 492, 1789],
        },
      ],

      /* Chart Tổng số hồ sơ */
      tongHS_chartOptions: {
        chart: {
          type: 'bar',
          height: 385,
          stacked: true,
          toolbar: false,
        },
        plotOptions: {
          bar: {
            horizontal: true,
          },
        },
        stroke: {
          width: 1,
          colors: ['#fff'],
        },
        xaxis: {
          categories: [
            'UBND TP Hà Nội',
            'UBND TP HCM',
            'UBND Tỉnh Đồng Nai',
            'UBND Tỉnh Bắc Ninh',
            'UBND Tỉnh Bắc Giang',
            'UBND Tỉnh Hà Tĩnh',
            'UBND TP Đà Nẵng',
            'UBND Tỉnh Bình Dương',
            'UBND Tỉnh Kiên Giang',
          ],
          labels: {
            formatter(val) {
              return `${val}`
            },
            style: {
              colors: ['#40566F'],
              fontSize: '14px',
              fontWeight: 400,
            },
          },
        },
        tooltip: {
          y: {
            formatter(val) {
              return `${val}`
            },
          },
        },
        fill: {
          opacity: 1,
        },
        colors: ['#C45FDD'],
        grid: {
          show: true,
          xaxis: {
            lines: {
              show: true,
            },
          },
          yaxis: {
            lines: {
              show: false,
            },
          },
          strokeDashArray: 5,
        },
      },
      tongHS_series: [
        {
          data: [1234, 521, 1231, 3234, 2527, 1478, 685, 945, 812],
        },
      ],

      /* Chart line */
      /* line_chartOptions: {
        chart: {
          height: 350,
          type: 'line',
          dropShadow: {
            enabled: true,
            color: '#000',
            top: 18,
            left: 7,
            blur: 10,
            opacity: 0.2,
          },
          animations: {
            enabled: true,
          },
          stacked: true,
          toolbar: false,
        },
        colors: ['#77B6EA', '#545454'],
        dataLabels: {
          enabled: true,
        },
        stroke: {
          curve: 'smooth',
        },
        grid: {
          borderColor: '#e7e7e7',
          row: {
            colors: ['#f3f3f3', 'transparent'],
            opacity: 0.5,
          },
          xaxis: {
            lines: {
              show: false,
            },
          },
          yaxis: {
            lines: {
              show: true,
            },
          },
          strokeDashArray: 5,
          top: 70,
          bottom: 50,
        },
        markers: {
          size: 1,
        },
        xaxis: {
          categories: ['2020', '2021'],
          tickPlacement: 'between',
        },
        yaxis: {
          min: 0,
          max: 100,
        },
        legend: {
          position: 'top',
          horizontalAlign: 'right',
          floating: true,
          offsetY: -25,
          offsetX: -5,
        },
      },
      line_series: [
        {
          name: '2020',
          data: [28, 59],
        },
        {
          name: '2021',
          data: [12, 31],
        },
      ], */
      line_chartOptions: {
        chart: {
          height: 350,
          type: 'line',
          animations: {
            enabled: true,
          },
          stacked: true,
          toolbar: false,
        },
        stroke: {
          width: [5, 5, 5],
          curve: 'straight',
        },
        labels: [2020, 2021],
        xaxis: {
          tickPlacement: 'between',
        },
        yaxis: {
          show: true,
          seriesName: ['0', '50%', '100%'],
        },
        grid: {
          show: true,
          xaxis: {
            lines: {
              show: false,
            },
          },
          yaxis: {
            lines: {
              show: true,
            },
          },
          strokeDashArray: 5,
          top: 70,
          bottom: 50,
        },
      },
      line_series: [
        {
          name: 'Chờ xử lý',
          data: [68, 43],
        },
        {
          name: 'Đang xử lý',
          data: [23, 46],
        },
      ],
    }
  },
}
</script>
<style lang="scss">
.hanh-chinh-cong {
  .title-box-chart {
    font-weight: 600;
    font-size: 20px;
    line-height: 24px;
    text-align: center;
    width: 100%;
    float: left;
    color: #40566f;
    margin-top: 15px;
  }
  .elm-data-dashboard {
    width: 100%;
    float: left;
    margin-top: 20px;
    .col-6:first-child {
      padding-left: 0;
    }
    .col-6:last-child {
      padding-right: 0;
    }
  }
  .title-hcc {
    width: 100%;
    float: left;
    font-weight: 600;
    font-size: 20px;
    line-height: 24px;
    color: #2b486a;
  }
  .table-data .card-body {
    padding: unset !important;
    .table-responsive {
      margin: 0;
    }
  }
  .table-data .card {
    margin: 0 !important;
  }
  .chart-content {
    width: 100%;
    float: left;
  }
  .data-chart-elm {
    width: 100%;
    float: left;
    background: #ffffff;
    border: 1px solid rgba(71, 95, 123, 0.2);
    border-radius: 6px;
  }
  .progress-data {
    width: 100%;
    float: left;
    padding: 25px;
  }
  .progress {
    border-radius: 3px !important;
    width: 100%;
    height: 35px;
  }
  .progress .progress-bar {
    cursor: pointer;
  }
  .progress .progress-bar:last-child {
    border-top-right-radius: 3px;
    border-bottom-right-radius: 3px;
  }
  .progress-bar span {
    font-style: normal;
    font-weight: 500;
    font-size: 14px;
    line-height: 18px;
    color: #ffffff;
  }
  .note-progress {
    width: 100%;
    float: left;
    padding-top: 20px;
    .note-elm-3 {
      width: 25%;
      float: left;
      .elm-square {
        height: 18px;
        width: 18px;
        float: left;
        vertical-align: middle;
        margin-top: 2px;
        border-radius: 2px;
      }
      span {
        vertical-align: middle;
        width: calc(100% - 18px);
        float: left;
        font-style: normal;
        font-weight: normal;
        font-size: 14px;
        line-height: 15px;
        color: #000000;
        padding-left: 7px;
        padding-top: 5px;
      }
    }
  }
  .elm-margin-custom {
    margin-top: 20px;
  }
  .table-data tbody tr td:nth-child(n + 3) {
    color: #ea5455;
  }
  .table-data tbody tr td:nth-child(n + 4) {
    color: #28c76f;
  }
}
</style>
