# wschedule 周日程

## components setup
```
npm i wschedule -S
```

### components use
``` html
<template>
  <div id="app">
    <WCalendar class="calendar"
               :isMultipleChoice="false"
               :pointMap="pointMap"
               :isSinglePoint="true"
               :restrictDate="restrictDate"
               :Month="month"
               @chooseDays="chooseDays"/>
  </div>
</template>
```
``` javascript
<script>
import Vue from 'vue'
import WSchedule from 'wschedule'
import "wschedule/dist/wschedule.css";
Vue.use(WSchedule)
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
     * 选择日期
     */
    chooseDays (row) {
      console.log(row)
    },
  },
}
</script>
```

### Attributes
|参数|说明|类型|可选值|默认值|
|---|---|---|---|---|
|isMultipleChoice|时间是连续选择还是间隔选择|Boolean| 1、true:单选，可间隔选多个； 2、false:连续选择|true
|Month|传入月份,用来显示传入月份的数据|String|--|--
|pointMap|显示需要加圆点的数据：用来表示某些日期是被使用|Object|数据格式为map { [new Date(具体的年月日).getTime()]:true}: 用年月日的时间戳为key|--
|restrictDate|是否禁止选择以前的日期 默认为空表示没有限制 注：如果只有数字则 默认时间是当天时间|Object|1、{1:['2022-02-11']}表示2022-02-11以前的日期不能选择；1：表示小于该时间的禁止选择，必填；2、{2:['2022-02-11']}表示2022-02-11以后的日期不能选择；2：表示大于该时间的禁止选择，必填；3、{3:['2022-02-11','2022-03-11']}表示2022-02-11到2022-03-11之间的日期可以选择；3：表示两个时间内的时间可以选择，必填；4、{4:['2022-02-11','2022-03-11']}表示2022-02-11到2022-03-11之外的日期可以选择；4：表示两个时间之外的可以选择，必填
|isSinglePoint|是否是单点，注：当isSinglePoint为true时，单点的权限高于isMultipleChoice(多选)，不可能单点又可以进行多选；默认是false，当为false时，就看是多选还是连续选择，看单点的权限高于isMultipleChoice|Boolean|1、true 单选，2：false:看多选|false
### Events
|名字|说明|类型|可选值|默认值|
|---|---|---|---|---|
|chooseDays|选择的时间|function|--|--

### 注意事项 Precautions
- 在点击日期的时候会有一个淡蓝色的背景hover效果，这个不是自己加上的，而是本身自带的，如何解决 在你需要点击的元素上，加上这样一行样式就可以了 ```-webkit-tap-highlight-color: transparent;```

 