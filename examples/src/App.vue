<template>
  <div id="app">
    <WCalendar class="calendar"
               :isMultipleChoice="false"
               :pointMap="pointMap"
               :restrictDate="restrictDate"
               :Month="month"
               @chooseDays="chooseDays"/>
  </div>
</template>

<script>

// import Vue from 'vue'
import WCalendar from '../../src/components/calendar'
// import "wqcalendar/dist/wqcalendar.css";
// Vue.use(WCalendar)

export default {
  name: 'App',
  components: {
    WCalendar
  },
  data () {
    /**
     * 获取当天时间
     * @returns {string}
     */
    function getCurDay () {
      var datetime = new Date()
      var year = datetime.getFullYear()
      var month = datetime.getMonth() + 1 < 10 ? '0' + (datetime.getMonth() + 1) : datetime.getMonth() + 1
      var date = datetime.getDate() < 10 ? '0' + datetime.getDate() : datetime.getDate()
      return `${year}-${month}-${date}`
    }

    return {
      month: '',
      pointMap: { [new Date(getCurDay()).getTime()]: true },
      restrictDate: { 1: [getCurDay()] }
    }
  },
  methods: {
    /**
     * 月份
     */
    monthValue (row) {
      console.log(row)
    },
    /**
     * 选择日期
     */
    chooseDays (row) {
      console.log(row)
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
