<template>
  <b-card
    v-if="tableData"
    no-body
    class="card-company-table"
  >
    <div class="d-flex align-items-center table-header">
      <div class="mr-auto">
        Lịch làm việc
      </div>
      <div>{{ currentDay }}</div>
    </div>
    <b-table
      :items="tableData"
      responsive
      :fields="fields"
      thead-class="hidden hide"
      class="mb-0"
    >
      <!-- company -->
      <template
        #cell(company)="data"
        class="column-1-dash"
      >
        <div class="d-flex align-items-center">
          <div>
            <div class="font-weight-bolder">
              {{ data.item.title }}
            </div>
            <div class="font-small-2 text-muted">
              {{ data.item.content }}
            </div>
          </div>
        </div>
      </template>

      <!-- time -->
      <template #cell(time)="data">
        <div class="d-flex flex-column">
          <span class="font-weight-bolder text-nowrap">{{
            data.item.dateTimeTo | formatTime
          }}</span>
        </div>
      </template>

      <!-- category -->
      <template
        #cell(category)="data"
        class="column-2-dash"
      >
        <span class="total-people-dash2">{{ data.item.totalPeople }}</span>

        <b-avatar-group
          size="35px"
          style="float: right"
        >
          <b-avatar
            v-for="(avatar, index) in data.item.avatarTitle"
            :key="index"
            :src="avatar"
            class="pull-up"
          />
        </b-avatar-group>
      </template>
    </b-table>
  </b-card>
</template>

<script>
import moment from 'moment'
import {
  BCard, BTable, BAvatar, BAvatarGroup,
} from 'bootstrap-vue'

export default {
  components: {
    BCard,
    BTable,
    BAvatar,
    BAvatarGroup,
  },
  filters: {
    formatTime(value) {
      if (!value) return ''
      return moment(value).format('D/MM/YYYY, hh:mm A')
    },
  },
  props: {
    tableData: {
      type: Array,
      default: () => [],
    },
  },

  data() {
    return {
      fields: [
        { key: 'company', label: 'Lịch làm việc' },
        { key: 'time', label: 'Thời gian' },
        { key: 'category', label: '' },
      ],
    }
  },
  computed: {
    currentDay() {
      return `Hôm nay, ${moment().format('DD/MM/YYYY')}`
    },
  },
}
</script>

<style lang="scss" scoped>
@import '~@core/scss/base/bootstrap-extended/include';
@import '~@core/scss/base/components/variables-dark';

.card-company-table ::v-deep td .b-avatar.badge-light-company {
  .dark-layout & {
    background: $theme-dark-body-bg !important;
  }
}
.total-people-dash2 {
  float: right;
  width: 45px;
  text-align: right;
  padding-top: 5px;
  font-weight: 500;
  font-size: 19.439px;
  line-height: 24px;
  color: #5e5873;
}
.table-header {
  background: #f3f2f7;
  text-transform: uppercase;
  font-weight: bold;
  font-size: 13px;
  padding: 0.72rem 2rem;
}
</style>
