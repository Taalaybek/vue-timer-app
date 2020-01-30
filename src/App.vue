<template>
  <v-app>
    <navbar :laps="laps" />
    <v-content>
      <timer @start="start" @lap="lap" @pause="pause" @goOn="goOn" @stop="stop" v-bind:timer="formattedTime" :state="timeState" />
    </v-content>
    <v-snackbar v-model="snackbar" color="info" :timeout="3500">
      New lap {{this.latestLap}} 
      <v-btn dark text @click="snackbar = false">Close</v-btn>
    </v-snackbar>

  </v-app>
</template>

<script>
import Navbar from '@/components/Navbar'
import Timer from '@/components/Timer'

export default {
  name: 'App',

  components: {
    Navbar, Timer
  },

  data: () => ({
    timeState: 'stopped',
    currentTimer: 0,
    formattedTime: "00:00:00",
    ticker: undefined,
    laps: [],
    latestLap: "",
    snackbar: false
  }),

  methods: {
    start() {
      if (this.timeState !== 'running') {
        this.tick()
        this.timeState = 'running'
      }
    },
    tick () {
      this.ticker = setInterval(()=>{
        this.currentTimer++;
        this.formattedTime = this.formatTime(this.currentTimer)
      }, 250)
    },

    formatTime(seconds) {
      let measuredTime = new Date(null)
      measuredTime.setSeconds(seconds)
      let MHSTime = measuredTime.toISOString().substr(11, 8)

      return MHSTime
    },

    lap() {
      this.snackbar=true
      this.laps.push({
        seconds: this.currentTimer,
        formattedTime: this.formatTime(this.currentTimer)
      })
      this.latestLap = this.formatTime(this.currentTimer)
      this.currentTimer = 0
    },
    
    pause() {
      window.clearInterval(this.ticker)
      this.timeState = 'paused'
    },

    stop() {
      window.clearInterval(this.ticker)
      this.currentTimer = 0
      this.formattedTime = "00:00:00"
      this.timeState = 'stopped'
    },

    goOn() {
      if (this.timeState === 'paused') {
        this.ticker = setInterval(() => {
          this.currentTimer++;
          this.formattedTime = this.formatTime(this.currentTimer)
        }, 250)
        this.timeState = 'running'
      }
    }
  }
};
</script>
