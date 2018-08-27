<template lang="html">
  <div class="container-fluid">
    <div class="row mt-2">
      <div class="col">
        <span class="display-4">{{ month }}</span>
        <span class="float-right mt-4" @click="toNext">{{ nextMonth }}</span>
        <table class="table table-bordered mt-3">
          <thead class="thead-dark">
            <tr>
              <th class="day">Sunday</th>
              <th class="day">Monday</th>
              <th class="day">Tuesday</th>
              <th class="day">Wednesday</th>
              <th class="day">Thursday</th>
              <th class="day">Friday</th>
              <th class="day">Saturday</th>
            </tr>
          </thead>
          <tbody>
            <tr class="week">
              <td class="lead">{{ weekOne(firstDay - 0) }}</td>
              <td class="lead">{{ weekOne(firstDay - 1) }}</td>
              <td class="lead">{{ weekOne(firstDay - 2) }}</td>
              <td class="lead">{{ weekOne(firstDay - 3) }}</td>
              <td class="lead">{{ weekOne(firstDay - 4) }}</td>
              <td class="lead">{{ weekOne(firstDay - 5) }}</td>
              <td class="lead">{{ weekOne(firstDay - 6) }}</td>
            </tr>
            <tr class="week">
              <td v-for="day in weekTwo" :key="day" class="lead">{{ day }}</td>
            </tr>
            <tr class="week">
              <td v-for="day in weekThree" :key="day" class="lead">{{ day }}</td>
            </tr>
            <tr class="week">
              <td v-for="day in weekFour" :key="day" class="lead">{{ day }}</td>
            </tr>
            <tr class="week">
              <td class="lead">{{ weekFive(lastDay - 0) }}</td>
              <td class="lead">{{ weekFive(lastDay - 1) }}</td>
              <td class="lead">{{ weekFive(lastDay - 2) }}</td>
              <td class="lead">{{ weekFive(lastDay - 3) }}</td>
              <td class="lead">{{ weekFive(lastDay - 4) }}</td>
              <td class="lead">{{ weekFive(lastDay - 5) }}</td>
              <td class="lead">{{ weekFive(lastDay - 6) }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import Moment from 'moment'
export default {
  data () {
    return {
      monthIndex: 0
    }
  },

  computed: {
    firstDay () {
      return Moment().add(this.monthIndex, 'months').startOf('month').day()
    },
    lastDay () {
      return Moment().add(this.monthIndex, 'months').endOf('month').day()
    },
    month () {
      return Moment().add(this.monthIndex, 'months').format('MMMM YYYY')
    },
    nextMonth () {
      return Moment().add(this.monthIndex + 1, 'months').format('MMMM YYYY')
    },
    prevMonth () {
      return Moment().subtract(this.monthIndex + 1, 'months').format('MMMM YYYY')
    },
    currentMonthLastDay () {
      return Moment().add(this.monthIndex, 'months').endOf('month').format('DD')
    },
    prevMonthLastDay () {
      return Moment().subtract(this.monthIndex + 1, 'months').endOf('month').format('DD')
    },
    saturdayDay () {
      return this.weekOne(this.firstDay - 6)
    },
    weekTwo () {
      let array = []
      for (let i = 1; i < 8; i++) {
        array.push(this.saturdayDay + i)
      }
      return array
    },
    weekThree () {
      let array = []
      for (let i = 8; i < 15; i++) {
        array.push(this.saturdayDay + i)
      }
      return array
    },
    weekFour () {
      let array = []
      for (let i = 15; i < 22; i++) {
        array.push(this.saturdayDay + i)
      }
      return array
    }
  },

  methods: {
    weekOne (n) {
      let last = this.prevMonthLastDay
      switch (n) {
        case 0:
          return 1
        case 1:
          return last
        case 2:
          return last - 1
        case 3:
          return last - 2
        case 4:
          return last - 3
        case 5:
          return last - 4
        case 6:
          return last - 5
        case -1:
          return 2
        case -2:
          return 3
        case -3:
          return 4
        case -4:
          return 5
        case -5:
          return 6
        case -6:
          return 7
      }
    },
    weekFive (n) {
      let last = this.currentMonthLastDay
      switch (n) {
        case 0:
          return last
        case 1:
          return last - 1
        case 2:
          return last - 2
        case 3:
          return last - 3
        case 4:
          return last - 4
        case 5:
          return last - 5
        case 6:
          return last - 6
        case -1:
          return 1
        case -2:
          return 2
        case -3:
          return 3
        case -4:
          return 4
        case -5:
          return 5
        case -6:
          return 6
      }
    }
  }
}
</script>

<style lang="css">
.day {
  width: 14.2857vw;
}
.list-group {
  font-size: .7rem;
  padding: 0;
  margin: 0;
}
.week {
  height: 15vh;
}
</style>
