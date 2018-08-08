<template>
  <div class="countdown-container">
    <div class="countdown-cells">
      <div class="countdown-cells__timer">
        {{daysTimer}}
      </div>
      <div class="countdown-cells__title">
        Days
      </div>
    </div>
    <div class="countdown-cells">
      <div class="countdown-cells__timer">
        {{hoursTimer}}
      </div>
      <div class="countdown-cells__title">
        Hours
      </div>
    </div>
    <div class="countdown-cells">
      <div class="countdown-cells__timer">
        {{minutesTimer}}
      </div>
      <div class="countdown-cells__title">
        Minutes
      </div>
    </div>
    <div class="countdown-cells">
      <div class="countdown-cells__timer">
        {{secondsTimer}}
      </div>
      <div class="countdown-cells__title">
        Seconds
      </div>
    </div>
  </div>
</template>

<script>
import * as timeEquivalences from '@/constants/time-conversion';

export default {
  name: 'CountDown',
  data(){
    return{
      daysTimer:undefined,
      hoursTimer:undefined,
      minutesTimer:undefined,
      secondsTimer:undefined,
      initialTimerInSeconds:undefined,
      timerID:undefined,
      remainingSeconds:undefined
    }
  }
  , props: {
    initialDays:{
      type: Number
      , default:0
    },
    initialHours:{
      type: Number
      , default:0
    },
    initialMinutes:{
      type: Number
      , default:0
    },
    initialSeconds:{
      type: Number
      , default:0
    }
  }
  , methods :{
    /**
     * Calculate the timer duration in seconds
     */
    calculateTimerDurationInSeconds(){
      this.initialTimerInSeconds = 
        (this.initialDays * timeEquivalences.DAY_IN_SECONDS) 
        + (this.initialHours * timeEquivalences.HOUR_IN_SECONDS) 
        + (this.initialMinutes * timeEquivalences.MINUTE_IN_SECONDS) 
        + this.initialSeconds;
      this.remainingSeconds = this.initialTimerInSeconds;
    }
    /**
     * Set the initial values for the elements (days, hours, minutes, seconds)
     */
    , displayInitialTime(){
      this.daysTimer = this.initialDays;
      this.hoursTimer = this.initialHours;
      this.minutesTimer = this.initialMinutes;
      this.secondsTimer = this.initialSeconds;
    }
    /**
     * Starts the timer component with the given input
     */ 
    , startTimer(){
      this.timerID = setInterval(()=>{
        this.updateTimer()
      },1000)
    }
    /**
     * Updates the view elements to display the timer's updates
     */
    , updateTimer(){
      //Validating if there isn't more remaining seconds
      if(this.remainingSeconds<0){
        clearInterval(this.timerID);
        console.info(`Timer Finished`)
        return;
      }
      console.info(`Remaining seconds => ${this.remainingSeconds}`)
      //Caculate Days, hours, minutes and seconds to display
      let temporalReminderSeconds = this.remainingSeconds;
      this.daysTimer=Math.floor(temporalReminderSeconds/timeEquivalences.DAY_IN_SECONDS);
      temporalReminderSeconds = temporalReminderSeconds%timeEquivalences.DAY_IN_SECONDS;
      this.hoursTimer=Math.floor(temporalReminderSeconds/timeEquivalences.HOUR_IN_SECONDS);
      temporalReminderSeconds = temporalReminderSeconds%timeEquivalences.HOUR_IN_SECONDS;
      this.minutesTimer=Math.floor(temporalReminderSeconds/timeEquivalences.MINUTE_IN_SECONDS);
      temporalReminderSeconds = temporalReminderSeconds%timeEquivalences.MINUTE_IN_SECONDS;
      this.secondsTimer=temporalReminderSeconds%timeEquivalences.MINUTE_IN_SECONDS;
      // Decreasing Remaning Seconds
      this.remainingSeconds--;
    }
    /**
     * Initialize the component's data
     */
    , initializeComponentData(){
      this.calculateTimerDurationInSeconds();
      this.displayInitialTime();
    }
  }
  /**
   * Initialize the component's data before it is shown
   */
  , created(){
    this.initializeComponentData()
  }
  /** 
   * Initialize the component after it has been mounted, so we don't miss anything :D!
  */
  , mounted(){
    this.startTimer()
  }
};
</script>

<style scoped>
.countdown-container{
  display:inline-block;
  position:relative;
  max-width: 500%;
}
.countdown-cells{
  float: left;
  display: block;
  width: 63px;
  padding:10px;
  margin:10px;
  border-style: solid;
  border-width: 1px;
  border-color: darkgrey;
  border-radius: 10px;
}
.countdown-cells__timer{
  font-size: x-large;
}
.countdown-cells__title{
  font-size: unset;
}
</style>

