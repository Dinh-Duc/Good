<template>
  <b-card
    v-if="data"
    no-body
    class="card-developer-meetup mb-0"
  >
    <div class="rounded-top">
      <span class="title-dash-trinh-ky">Văn bản trình ký</span>
    </div>

    <b-card-body class="px-0">
      <!-- metting header -->
      <div class="meetup-header d-flex align-items-center">
        <div class="meetup-day">
          <h6 class="mb-0">
            THU
          </h6>
          <h3 class="mb-0">
            24
          </h3>
        </div>
        <div class="my-auto text-base text-left">
          Bạn có 12 văn bản trình ký
        </div>
      </div>
      <!--/ metting header -->
      <vue-perfect-scrollbar
        :settings="perfectScrollbarSettings"
        class="sidebar-menu-list scroll-area"
        style="max-height: 240px"
      >
        <ul class="dasboard2-ul-vb">
          <li
            v-for="(dataDocs, index) in dataListDocs"
            :key="index"
            class="d-flex align-items-center"
          >
            <div
              class="img-trinh-ky-dash d-flex align-items-center justify-content-center"
            >
              <b-img :src="dataDocs.imgTrinhKy" />
            </div>
            <div class="elm-vb-db d-flex flex-fill">
              <div class="flex-fill text-left">
                <b>{{ dataDocs.title }}</b>
                <div>{{ dataDocs.content }}</div>
              </div>
              <div class="text-right ml-auto date-trinh-ky">
                {{ dataDocs.time }}
              </div>
            </div>
          </li>
        </ul>
      </vue-perfect-scrollbar>
    </b-card-body>
  </b-card>
</template>

<script>
import {
  BCard,
  BImg,
  BCardBody,
  /* BCardText, */
  BCardTitle,
  /* BMedia, BMediaAside,  BAvatar,
  BAvatarGroup, */
  VBTooltip,
  /* BMediaBody, */
} from 'bootstrap-vue'
import VuePerfectScrollbar from 'vue-perfect-scrollbar'

export default {
  components: {
    BCard,
    BImg,
    BCardBody,
    /* BCardText, */
    BCardTitle,
    /*  BMedia,
    BMediaAside,
    BAvatar,
    BAvatarGroup, */
    VuePerfectScrollbar,
    /* BMediaBody, */
  },
  directives: {
    'b-tooltip': VBTooltip,
  },
  props: {
    data: {
      type: Object,
      default: () => {},
    },
  },
  data() {
    return {
      dataListDocs: [
        {
          imgTrinhKy: require('@/assets/images/dashboard2/vb-trinh-ky.png'),
          title: 'Vụ Kế hoạch - Tài chính trình ký',
          content:
            'Tờ trình phê duyệt chủ trương đầu tư dự án đầu tư xây dựng trạm quan trắc nước tại miền Trung',
          time: '10:00 AM',
        },
        {
          imgTrinhKy: require('@/assets/images/dashboard2/vb-trinh-ky.png'),
          title: 'Văn phòng Bộ trình ký',
          content:
            'Công văn về việc ứng dụng phần mềm quản lý điểm danh vào sử dụng tại Bộ TNMT',
          time: '15:30 AM',
        },
        {
          imgTrinhKy: require('@/assets/images/dashboard2/vb-trinh-ky.png'),
          title: 'Tổng cục Địa chất và Khoáng sản trình ký',
          content:
            'Dự thảo Ban hành quy định mới về khai thác khoáng sản',
          time: '11:00 AM',
        },
        {
          imgTrinhKy: require('@/assets/images/dashboard2/vb-trinh-ky.png'),
          title: 'Ban quản lý các dự án đầu tư xây dựng trình ký',
          content:
            'Dự thảo trình chính phủ về quy hoạch sử dụng đất thành phố Hà Nội giai đoạn 2021-2025',
          time: '08:40 AM',
        },
        {
          imgTrinhKy: require('@/assets/images/dashboard2/vb-trinh-ky.png'),
          title: 'Văn phòng Bộ trình ký',
          content:
            'Ban hành chương trình chuyển đổi số ngành tài nguyên môi trường',
          time: '09:00 AM',
        },
      ],
      perfectScrollbarSettings: {
        maxScrollbarLength: 60,
      },
    }
  },
}
</script>
<style lang="scss">
.dasboard2-ul-vb {
  padding: 0;
}
ul.dasboard2-ul-vb li {
  width: 100%;
  margin-bottom: 15px;
  display: block;
}
span.title-dash-trinh-ky {
  font-weight: 500;
  font-size: 18px;
  line-height: 30px;
}

.img-trinh-ky-dash {
  width: 48px;
  height: 48px;
  min-width: 48px;
  text-align: center;
  background: rgba(115, 103, 240, 0.12);
  border-radius: 6px;
}
.date-trinh-ky {
  min-width: 70px;
}
.elm-vb-db {
  padding-left: 15px;
}
.elm-vb-db div b {
  font-weight: 500;
  font-size: 15px;
  color: #5e5873;
}
.elm-vb-db div span {
  width: 80px;
  text-align: right;
}

.dark-layout {
  span.title-dash-trinh-ky {
    color: #d0d2d6;
  }
  .elm-vb-db b {
    color: #fff;
  }
}
</style>
