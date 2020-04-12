<template>
  <q-page class="flex flex-center">
    <q-table title="Weather" :data="forecasts" :columns="forecastCols"></q-table>
  </q-page>
</template>

<script>
import { date } from 'quasar'
import axios from 'axios';

export default {
  name: 'PageIndex',
  data()
  {
    return {
      forecasts: [{ summary: 'No data.' }],
      forecastCols: [
        { name: 'Summary', label: 'Summary', field: (row) => row.summary },
        { name: 'F', label: 'F', field: (row) => row.temperatureF },
        { name: 'C', label: 'C', field: (row) => row.temperatureC },
        { name: 'Date', label: 'Date', field: (row) => row.date, format: (val) => `${date.formatDate(val, 'YYYY/MM/DD HH:mm:ss')}` }
      ]
    }
  },
  async mounted()
  {
    try
    {
      this.forecasts = (await axios.get('api/weatherforecast')).data;
    }

    catch
    {
      this.forecasts = [{ summary: 'No data.' }];
    }
  }
}
</script>
