<template>
  <div>
    <div class="layout-padding">
      <h5>Date & Datetime</h5>
      <div class="group">
        <div class="label bg-secondary text-white">
          From <span class="right-detail"><em>{{first.range.from}}</em></span>
        </div>
        <div class="label bg-secondary text-white">
          To <span class="right-detail"><em>{{first.range.to}}</em></span>
        </div>
        <br>
        <div class="label bg-secondary text-white">
          Min <span class="right-detail"><em>{{first.min}}</em></span>
        </div>
        <div class="label bg-secondary text-white">
          Max <span class="right-detail"><em>{{first.max}}</em></span>
        </div>
      </div>
      <p class="caption">
        Date Range
      </p>
      <q-datetime-range type="date" v-model="first.range" :min="first.min" :max="first.max" />
      <p class="caption">
        Datetime Range
      </p>
      <q-datetime-range type="datetime" v-model="first.range" :min="first.min" :max="first.max" />

      <br>
      <h5>Time</h5>
      <div class="group">
        <div class="label bg-secondary text-white">
          From <span class="right-detail"><em>{{second.range.from}}</em></span>
        </div>
        <div class="label bg-secondary text-white">
          To <span class="right-detail"><em>{{second.range.to}}</em></span>
        </div>
        <br>
        <div class="label bg-secondary text-white">
          Min <span class="right-detail"><em>{{second.min}}</em></span>
        </div>
        <div class="label bg-secondary text-white">
          Max <span class="right-detail"><em>{{second.max}}</em></span>
        </div>
      </div>
      <p class="caption">
        Time Range
      </p>
      <q-datetime-range type="time" v-model="second.range" :min="second.min" :max="second.max" />

      <br>
      <h5>Optional CSS</h5>
      <p class="caption">CSS class 'full-width'</p>
      <q-datetime-range class="full-width" type="time" v-model="second.range" :min="second.min" :max="second.max" />
    </div>
  </div>
</template>

<script>
const day = new Date('2016-10-24T10:40:14.674Z')

export default {
  data () {
    return {
      first: {
        min: new Date(day).setDate(day.getDate() - 5),
        max: new Date(new Date(new Date(day).setDate(day.getDate() + 1)).setHours(day.getHours() + 4)).setMinutes(day.getMinutes() + 10),
        range: {
          from: new Date(day).setDate(day.getDate() - 3),
          to: new Date(new Date(new Date(day).setMonth(day.getMonth() + 1)).setHours(day.getHours() + 4)).setMinutes(day.getMinutes() + 10)
        }
      },
      second: {
        min: new Date(new Date().setHours(3)).setMinutes(15),
        max: new Date(new Date().setHours(22)).setMinutes(32),
        range: {
          from: null,
          to: null
        }
      }
    }
  }
}
</script>
