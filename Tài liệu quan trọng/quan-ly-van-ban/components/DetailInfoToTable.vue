<template lang="">
  <div class="detail-in-table-prt">
    <div class="child-detail-in-table-prt">
      <b-table
        sticky-header
        striped
        hover
        :items="fakeItems"
        :fields="fields"
        :fixed="true"
        :current-page="currentPage"
        @row-clicked="chooseItemInTable"
      />
    </div>
    <div class="paging-prt">
      <div class="center-paging">
        <b-pagination
          v-if="TotalPage > 0 && TotalItems > 10"
          v-model="currentPage"
          :total-rows="TotalItems"
          :first-number="true"
          :last-number="true"
          align="fill"
          size="sm"
          class="my-0"
          @input="changePageAndGetDocs(currentPage)"
        />
      </div>
    </div>
  </div>
</template>
<script>
import { mapGetters } from 'vuex'

export default {
  props: {
    changeTab: {
      type: Boolean,
      default: null,
    },
  },
  data() {
    return {
      fields: [
        {
          key: 'ngayNhan',
          label: 'NGÀY NHẬN',
          thClass: 'ngay-nhan',
        },
        {
          key: 'soKyHieu',
          label: 'SỐ/KÝ HIỆU',
          thClass: 'so-ky-hieu',
        },
        {
          key: 'ngayBanHanh',
          label: 'NGÀY BAN HÀNH',
          thClass: 'ngay-ban-hanh',
        },
        {
          key: 'trichYeu',
          label: 'TRÍCH YẾU',
          thClass: 'trich-yeu',
        },
        {
          key: 'coQuanBanHanh',
          label: 'CƠ QUAN BAN HÀNH',
          thClass: 'co-quan-ban-hanh',
        },
        {
          key: 'trangThai',
          label: 'TRẠNG THÁI',
          thClass: 'trang-thai',
        },
      ],
      currentPage: this.$store.state.docsManage.CurrentPage,
      fakeItems: [],
    }
  },
  computed: mapGetters([
    'ListDocs',
    'TotalPage',
    'TotalItems',
    'Param',
    'ChangeTab',
  ]),
  watch: {
    ChangeTab() {
      if (this.ChangeTab === false || this.ChangeTab === true) this.currentPage = 1
      if (!this.fakeItems.length) this.getItems()
    },
  },
  created() {
    this.getItems()
  },
  methods: {
    changePageAndGetDocs(page) {
      const model = {
        DocTypeId: this.Param.loaiVanBan,
        TinhTrang: this.Param.maTinhTrang,
        TrangThai: this.Param.maTrangThai,
        TrangThaiVanBan: this.Param.trangThaiVanBan,
        PageIndex: page,
      }
      console.log(model)
      this.$emit('item-page-clicked', model)
    },

    chooseItemInTable(e) {
      this.$emit('choose-item', e)
    },
    getItems() {
      window
        .COMMON_POST2(
          'http://45.117.83.218:5004/api/VanBan/search_all_vanban',
          {
            fromNgayDen: '01/01/2021 00:00:00',
            fromNgayVB: '',
            keyword: '',
            loaiVanBan: 1,
            maTinhTrang: '',
            maTrangThai: '',
            noiBanHanh: '',
            noiNhan: '',
            pageIndex: 1,
            pageSize: 10,
            timeFormat: 'dd/MM/yyyy HH:mm:ss',
            toNgayDen: '31/12/2021 00:00:00',
            toNgayVB: '',
          },
        )
        .then(res => {
          console.log(13123, res)

          this.fakeItems = res.pageData.map(i => ({
            ngayNhan: i.ngayDen,
            soKyHieu: i.soKyHieu,
            ngayBanHanh: i.ngayDen,
            trichYeu: i.trichYeu,
            coQuanBanHanh: i.noiBanHanh,
            trangThai: 'Xử lý',
          }))
          console.log(13123, this.fakeItems)
        })
    },
  },
}
</script>
<style lang="scss">
.docs-manage {
  .table-list-docs {
    width: 100%;
    float: left;
    height: calc(100% - 163px);
  }
  .paging-prt {
    text-align: center;
    width: 100%;
    padding-top: 10px;
    float: left;
  }
  .center-paging {
    width: 600px;
    margin: 0 auto;
  }
  .detail-in-table-prt {
    padding: 0 15px;
    width: 100%;
    float: left;
    padding-top: 10px;
    height: 100%;
  }
  .child-detail-in-table-prt {
    border-radius: 6px;
    border: 1px solid rgba(71, 95, 123, 0.2);
    width: 100%;
    overflow: hidden;
    height: 100%;
  }
  .detail-in-table-prt table {
    width: 100%;
    float: left;
    margin: 0;
  }
  .detail-in-table-prt table thead tr th {
    padding: 21px 10px !important;
  }
  th.ngay-nhan {
    width: 10%;
    text-align: center;
  }
  th.so-ky-hieu {
    width: 15%;
    text-align: center;
  }
  th.ngay-ban-hanh {
    width: 13%;
    text-align: center;
  }
  th.trich-yeu {
    width: 28%;
    text-align: center;
  }
  th.co-quan-ban-hanh {
    width: 15%;
    text-align: center;
  }
  th.trang-thai {
    width: 20%;
    text-align: center;
  }

  .detail-in-table-prt .b-table-sticky-header {
    overflow-y: auto;
    max-height: unset;
    margin: 0;
    height: 100%;
  }
  /* width */
  .b-table-sticky-header::-webkit-scrollbar {
    width: 10px;
  }

  /* Track */
  .b-table-sticky-header::-webkit-scrollbar-track {
    background: white;
  }

  /* Handle */
  .b-table-sticky-header::-webkit-scrollbar-thumb {
    background: rgb(201, 198, 198);
    border-radius: 5px;
  }

  /* Handle on hover */
  .b-table-sticky-header::-webkit-scrollbar-thumb:hover {
    background: rgb(163, 163, 163);
  }
}
</style>
