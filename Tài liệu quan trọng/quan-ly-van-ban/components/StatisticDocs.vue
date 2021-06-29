<template>
  <div class="statistic-prt">
    <div class="title-docs-chart">
      <b>{{ title }}</b>
    </div>
    <div class="list-statistics-detail">
      <div
        v-for="(data, index) in DepartmentMiss"
        :key="index"
        class="elm-statistics"
      >
        <span class="title-elm-statistic-doc">{{ data.name }}</span>
        <div class="progress-form">
          <b-progress>
            <b-progress-bar
              :value="data.value"
              :style="{ 'background-color': '#EB5757' }"
            >
              <span>{{ data.value }}</span>
            </b-progress-bar>
          </b-progress>
        </div>
        <p class="total-elm-statistic">
          {{ data.max }}
        </p>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'StatisticDocs',
  props: {
    title: {
      type: String,
      default: '',
    },
  },
  data() {
    return {
      DepartmentMiss: [
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
    }
  },
}
</script>
<style lang="scss" scoped>
.docs-manage {
  .statistic-prt {
    width: 100%;
    height: 210%;
    float: left;
    background: #ffffff;
    border: 1px solid #e0e0e0;
    border-radius: 10px;
    padding: 8px 12px 0px 12px;
  }
  .progress {
    height: 15px;
    border-radius: 3px !important;
  }
  .progress-bar {
    border-radius: 3px !important;
  }
  .statistic-prt .progress .progress-bar:last-child {
    border-top-right-radius: 3px !important;
    border-bottom-right-radius: 3px !important;
  }
  .progress-form {
    width: calc(100% - 240px);
    float: left;
  }
  .list-statistics-detail {
    width: 100%;
    float: left;
  }
  .preview-prt-statistic .statistic-prt {
    overflow-y: auto !important;
    padding-bottom: 10px;
  }
  /* width */
  .preview-prt-statistic .statistic-prt::-webkit-scrollbar {
    width: 10px;
    border-radius: 20px !important;
  }

  /* Track */
  .preview-prt-statistic .statistic-prt::-webkit-scrollbar-track {
    background: white;
    border-radius: 10px;
  }

  /* Handle */
  .preview-prt-statistic .statistic-prt::-webkit-scrollbar-thumb {
    background: rgb(201, 198, 198);
    border-radius: 10px !important;
  }

  /* Handle on hover */
  .preview-prt-statistic
    .statistic-prt::-webkit-scrollbar-thumb:hover {
    background: rgb(163, 163, 163);
    border-radius: 10px !important;
  }
  .elm-statistics {
    margin-top: 10px;
    width: 100%;
    float: left;
  }
  .title-elm-statistic-doc {
    width: 175px;
    float: left;
    font-style: normal;
    font-weight: normal;
    font-size: 12px;
    line-height: 15px;
    color: #4f4f4f;
  }
  .statistic-prt .bg-danger {
    background: #eb5757;
    border-radius: 3px !important;
    font-style: normal;
    font-weight: 500;
    font-size: 14px;
    line-height: 18px;
    color: #ffffff;
  }
  .progress-bar span {
    font-style: normal;
    font-weight: 500;
    font-size: 10px;
    line-height: 18px;
    color: #ffffff;
  }

  /* Mới */
  .title-docs-chart {
    width: 100%;
    float: left;
    border-bottom: 1px solid #828282;
    b {
      width: 100%;
      float: left;
      font-style: normal;
      font-weight: 600;
      font-size: 16px;
      line-height: 20px;
      color: #000000;
      padding-bottom: 1px;
    }
  }
  .total-elm-statistic {
    margin: 0 !important;
    width: 65px;
    padding-left: 30px;
    float: left;
    font-style: normal;
    font-weight: normal;
    font-size: 12px;
    line-height: 15px;
    color: #4f4f4f;
    padding-top: 3px;
  }
}
</style>
