<template>
  <table>
    <thead>
    <tr>
      <th>#</th>
      <th>{{'History_TableAmount' | localize}}</th>
      <th>{{'Currency_TableDate' | localize}}</th>
      <th>{{'History_TableCategory' | localize}}</th>
      <th>{{'History_TableType' | localize}}</th>
      <th>{{'History_TableOpen' | localize}}</th>
    </tr>
    </thead>

    <tbody>
    <tr v-for="(record, index) of records" :key="index">
      <td>{{ index + 1 }}</td>
      <td>{{ record.amount | currency('RUB') }}</td>
      <td>{{ record.date | date('datetime') }}</td>
      <td>{{ record.categoryName }}</td>
      <td>
        <span 
        :class="[record.typeClass]"
        class="white-text badge red"
        >{{ record.typeText }}</span>
      </td>
      <td>
        <button 
          class="btn-small btn" 
          @click="$router.push('/detail/' + record.id)"
          v-tooltip="'Посмотреть запись'"
        >
          <i class="material-icons">open_in_new</i>
        </button>
      </td>
    </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    records: {
      required: true,
      type: Array
    }
  }
}
</script>
