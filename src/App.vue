<template>
  <div id="app">
    <span>{{time}}</span>
    <br>
    <button 
    @click="test">인증번호 전송
    </button>
  </div>
</template>

<script>
import moment from 'moment'

const startTime = '00:03:00'
const mmssFormat = 'mm:ss'
const timeFormat = 'hh:mm:ss'

// const a = {
//   name: '1',  
//   data: () => {
//     console.log(this)
//     return 'a'
//   },
//   data2 () {
//     console.log(this)
//     return 'b'
//   }
// }

export default {
  name: 'App',
  data() {
    return {
      time: moment(startTime, timeFormat).format(mmssFormat),
      timer_instance: null,
      timer_restart: true
    }
  },
  methods: {
    test() {
      if (this.timer_instance) {
        clearInterval(this.timer_instance)
        this.timer_restart = !this.timer_restart
      }
      this.timer_instance = setInterval(this.min, 1000) 

      if (!this.timer_restart) {
        this.time = moment(startTime, timeFormat).format(mmssFormat)
        clearInterval(this.timer_instance)
      }
    },
    min() {
      if (this.time !== "00:00") {
        this.time = moment(this.time, mmssFormat).subtract(1, "second").format(mmssFormat)
        console.log(this.timer_restart)
      } else {
        document.body.style.backgroundColor = "red"
      }
    }
  }
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
#app span{
  font-size: 50px;
}

.go{
  color:green;
}
.stop{
  color:red
}

</style>
