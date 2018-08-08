<template>
  <div id="app">
    <h2>Countdown Timer</h2>
    <h3>First Example</h3>
    <count-down
      :initialDays="1"
      :initialHours="23"
      :initialMinutes="27"
      :initialSeconds="47">
    </count-down>
    <h3>Second Example</h3>
    <count-down
      :initialDays="1"
      :initialMinutes="1"
      :initialSeconds="8">
    </count-down>
  </div>
</template>
<script>
import CountDown from '@/components/CountDown.vue';

export default {
  name: 'app',
  components:{
    CountDown
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
