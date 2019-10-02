<template>
  <div>
    <Loader v-if="loading" />
    <div v-else-if="record">
      <div class="breadcrumb-wrap">
        <router-link to="/history" class="breadcrumb">Menu_History</router-link>
        <a @click.prevent class="breadcrumb">
          {{ record.type === 'income' ? 'History_Income' : 'History_Outcome' | localize }}
        </a>
      </div>
      <div class="row">
        <div class="col s12 m6">
          <div 
            class="card"
            :class="{
              'red': record.type === 'outcome',
              'green': record.type === 'income'
            }"
          >
            <div class="card-content white-text">
              <p>{{'Records_Description' | localize}}: {{record.description}}</p>
              <p>{{'History_TableAmount' | localize}}: {{record.amount| currency}}</p>
              <p>{{'Category' | localize}}: {{record.categoryName}}</p>

              <small>{{record.date | date('datetime')}}</small>
            </div>
          </div>
        </div>
      </div>
    </div>
    <p class="center" v-else>Запись с id: <strong>{{$route.params.id}}</strong> не найдена</p> 
  </div>
</template>

<script>
import localizeFilter from '@/filters/localize.filter'

export default {
  name: 'detail',
  metaInfo() {
    return {
      title: this.$title('DetailsTitle')
    }
  },
  data: () => ({
    record: null,
    loading: true
  }),
  async mounted() {
    const id = this.$route.params.id
    const record = await this.$store.dispatch('fetchRecordById', id)
    const category = await this.$store.dispatch('fetchCategoryById', record.categoryID)

    this.record = {
      ...record,
      categoryName: category.title
    }


    this.loading = false
  }
}
</script>
