<template>
  <v-row justify="center">
    <v-date-picker

        ref="picker"
        v-model="date"
        :picker-date.sync="pickerDate"

      :allowed-dates="allowedDates"
      class="mt-4"
      min="2016-06-15"
      max="date"
    ></v-date-picker>
  </v-row>
</template>

<script>
  export default {
    data: () => ({
      date: '2018-03-02',
    }),

    methods: {
      allowedDates: val => parseInt(val.split('-')[2], 10) % 2 === 0,
    },
  }
</script>