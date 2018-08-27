<template lang="html">
  <div class="container-fluid">
    <div class="row mt-2">
      <div class="col">
        <span class="display-4">{{ month }}</span>
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
              <td class="lead">1</td>
              <td class="lead">2</td>
              <td class="lead">3</td>
              <td class="lead">4</td>
              <td class="lead">5</td>
              <td class="lead">6</td>
              <td class="lead">7</td>
            </tr>
            <tr class="week">
              <td class="lead">8</td>
              <td class="lead">9</td>
              <td class="lead">10</td>
              <td class="lead">11</td>
              <td class="lead">12</td>
              <td class="lead">13</td>
              <td class="lead">14</td>
            </tr>
            <tr class="week">
              <td class="lead">15</td>
              <td class="lead">16</td>
              <td class="lead">17</td>
              <td class="lead">18</td>
              <td class="lead">19</td>
              <td class="lead">20</td>
              <td class="lead">21</td>
            </tr>
            <tr class="week">
              <td class="lead">22</td>
              <td class="lead">23</td>
              <td class="lead">24</td>
              <td class="lead">25</td>
              <td class="lead">26</td>
              <td class="lead">27</td>
              <td class="lead">28</td>
            </tr>
            <tr class="week">
              <td class="lead">29</td>
              <td class="lead">30</td>
              <td class="lead">31</td>
              <td class="lead">1</td>
              <td class="lead">2</td>
              <td class="lead">3</td>
              <td class="lead">4</td>
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

    }
  },

  computed: {
    month () {
      return Moment().format('MMMM YYYY')
    }
  }
}
</script>

<style lang="css">
.day {
  width: 14.2857%;
}
.week {
  height: 15vh;
}
</style>
