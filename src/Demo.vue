<template>
  <div id="app">

    <h1>Datepicker Examples</h1>

    <div class="example">
      <h3>Default datepicker</h3>
      <datepicker v-model="vModelExample" ref="datepicker" :dateText="dateText" :disabled="{}" @selected="validaDate" :validate="validate"></datepicker>
      <button @click="$refs.datepicker.open()">打开</button>
    </div>
  </div>
</template>

<script>
import Datepicker from '@/components/Datepicker'
import DateLanguages from '@/utils/DateLanguages'

const state = {
  date1: new Date()
}

export default {
  name: 'app',
  components: {
    Datepicker
  },
  data () {
    return {
      format: 'd MMMM yyyy',
      disabled: {},
      eventMsg: null,
      state: state,
      language: 'en',
      languages: DateLanguages.translations,
      vModelExample: null,
      inline: true,
      dateText: [
        {
          date: '2017-07-10',
          text: '余5'
        },
        {
          date: '2017-07-11',
          text: '余6'
        }
      ]
    }
  },
  methods: {
    alter () {
      console.log('座位不足')
    },
    validate (day) {
      if (day.text && day.text.slice(1) < 6) {
        this.alter()
        return false
      }
      return true
    },
    validaDate (day) {
      if (!day.text) {
        return
      }
      if (day.text.slice(1) < 6) {
        console.log('座位不足')
        this.$refs.datepicker.open()
        return
      }
    },
    disableTo (val) {
      if (typeof this.disabled.to === 'undefined') {
        this.disabled = {
          to: null,
          from: this.disabled.from
        }
      }
      this.disabled.to = val
    },
    disableFrom (val) {
      if (typeof this.disabled.from === 'undefined') {
        this.disabled = {
          to: this.disabled.to,
          from: null
        }
      }
      this.disabled.from = val
    }
  }
}
</script>

<style>

body {
    font-family: 'Helvetica Neue Light', Helvetica, sans-serif;
    padding: 1em 2em 2em;
}
input, select {
    padding: .75em .5em;
    font-size: 100%;
    border: 1px solid #ccc;
    width: 100%
}

select {
    height: 2.5em;
}

.example {
    background: #f2f2f2;
    border: 1px solid #ddd;
    padding: 0em 1em 1em;
    margin-bottom: 2em;
}

code,
pre {
    margin: 1em 0;
    padding: 1em;
    border: 1px solid #bbb;
    display: block;
    background: #ddd;
    border-radius: 3px;
}

.settings {
    margin: 2em 0;
    border-top : 1px solid #bbb;
    background: #eee;
}

h5 {
    font-size:100%;
    padding: 0;
}

.form-group {
    margin-bottom: 1em;
}

.form-group label {
    font-size: 80%;
    display: block;
}
</style>
