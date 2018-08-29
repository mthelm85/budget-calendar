<template lang="html">
  <transition name="fade" mode="out-in">
    <div class="container-fluid" :key="monthIndex">
      <div class="row mt-2">
        <div class="col">
          <span class="display-4">{{ month }}</span>
          <span class="float-right mt-4">
            <button class="btn btn-outline-dark" @click="monthIndex--">{{ prevMonth }}</button>
            <button class="btn btn-outline-dark" @click="monthIndex++">{{ nextMonth }}</button>
          </span>
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
                <td class="lead" ref="day1">{{ weekOne(firstDay - 0) }}</td>
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
              <tr v-if="!extraRow" class="week">
                <td class="lead">{{ weekLast(lastDay - 0) }}</td>
                <td class="lead">{{ weekLast(lastDay - 1) }}</td>
                <td class="lead">{{ weekLast(lastDay - 2) }}</td>
                <td class="lead">{{ weekLast(lastDay - 3) }}</td>
                <td class="lead">{{ weekLast(lastDay - 4) }}</td>
                <td class="lead">{{ weekLast(lastDay - 5) }}</td>
                <td class="lead">{{ weekLast(lastDay - 6) }}</td>
              </tr>
              <tr v-if="extraRow" class="week">
                <td v-for="day in weekFiveOfSix" :key="day" class="lead">{{ day }}</td>
              </tr>
              <tr v-if="extraRow" class="week">
                <td class="lead">{{ weekLast(lastDay - 0) }}</td>
                <td class="lead">{{ weekLast(lastDay - 1) }}</td>
                <td class="lead">{{ weekLast(lastDay - 2) }}</td>
                <td class="lead">{{ weekLast(lastDay - 3) }}</td>
                <td class="lead">{{ weekLast(lastDay - 4) }}</td>
                <td class="lead">{{ weekLast(lastDay - 5) }}</td>
                <td class="lead">{{ weekLast(lastDay - 6) }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </transition>
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
    /* Some months require 6 rows to display all of their days. This function
       determines whether or not this is the case. */
    extraRow () {
      if (this.firstDay >= 5 && this.daysInMonth === 31) {
        return true
      } else if (this.firstDay === 6 && this.daysInMonth === 30) {
        return true
      }
    },
    daysInMonth () {
      return Moment().add(this.monthIndex, 'months').daysInMonth()
    },
    firstDay () {
      return Moment().add(this.monthIndex, 'months').startOf('month').day()
    },
    lastDay () {
      return Moment().add(this.monthIndex, 'months').endOf('month').day()
    },
    currentMonthLastDay () {
      return Moment().add(this.monthIndex, 'months').endOf('month').format('DD')
    },
    prevMonthLastDay () {
      return Moment().subtract(Math.abs(this.monthIndex) + 1, 'months').endOf('month').format('DD')
    },
    month () {
      return Moment().add(this.monthIndex, 'months').format('MMMM YYYY')
    },
    nextMonth () {
      return Moment().add(this.monthIndex + 1, 'months').format('MMM YYYY')
    },
    prevMonth () {
      return Moment().subtract(Math.abs(this.monthIndex) + 1, 'months').format('MMM YYYY')
    },
    /* This function determines the correct day (number) for Saturday of the
       first week. This value is used to set the values for the days in weeks
       two thru four (see weekTwo, weekThree, weekFour below) */
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
    },
    /* When six rows of weeks are needed for the month, this function calculates
       the values for week five */
    weekFiveOfSix () {
      let array = []
      for (let i = 22; i < 29; i++) {
        array.push(this.saturdayDay + i)
      }
      return array
    }
  },

  methods: {
    /* Determine the dates for the first week, based on the last day of the
       previous month */
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
    /* Determine the dates for the last week, based on the last day of the
       current month */
    weekLast (n) {
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
td:hover {
  background-color: #efefef;
}
.week {
  height: 15vh;
}
</style>
