<template>
  <div id="app">

    <div style="width: 896px; height: 529px; position: relative">
      <!--        date de maintenant-->

      <div
          style="left: 0px; top: 0px; position: absolute; color: #415C73; font-size: 30px; font-family: Roboto; font-weight: 900; word-wrap: break-word">
        {{ currentDate }}
      </div>

      <!--        start button-->
      <div class="button start-button" @click="startTimer" style="background: white;color:#60B669 ">

        <div style="width: 126px; height: 38px; left: 651px; top: 3px; position: absolute">
          <div
              style="width: 13px; height: 15.89px; left: 12px; top: 11px; position: absolute; background: #60B669"></div>
          <div
              style="width: 126px; height: 38px; left: 0px; top: 0px; position: absolute; border-radius: 5px; border: 0.50px #60B669 solid"></div>
          <div class="button start-button" @click="startTimer" style="background: white;color:#60B669 ">

            Start Now
          </div>
        </div>
      </div>
      <!--        stop button-->
      <div class="button stop-button" @click="stopTimer" style="background: white;color:#60B669 ">


        <div style="width: 86px; height: 38px; left: 552px; top: 2px; position: absolute">
          <div
              style="width: 86px; height: 38px; left: 0px; top: 0px; position: absolute; border-radius: 5px; border: 0.50px #CC5252 solid"></div>
          <div style="width: 63px; height: 22px; left: 11px; top: 9px; position: absolute">
            <div
                style="left: 23px; top: 0px; position: absolute; color: #CC5252; font-size: 19px; font-family: Roboto; font-weight: 500; word-wrap: break-word">
              Stop
            </div>
          </div>
          <div style="width: 12px; height: 12px; left: 0px; top: 4px; position: absolute; background: #CC5252"></div>
        </div>
      </div>
<!--      timer-->
      <div style="left: 809px; top: 8px; position: absolute"><span
          style="color: #60B669; font-size: 25px; font-family: Roboto; font-weight: 900; word-wrap: break-word">{{
          formattedPeriod
        }}</span></div>
<!--      début du tableau-->
      <div style="width: 895px; height: 227px; left: 0px; top: 137px; position: absolute">
        <!--          début du tableau-->
        <div
            style="width: 895px; height: 0px; left: 895px; top: 0px; position: absolute; transform: rotate(-180deg); transform-origin: 0 0; border: 0.50px #60B669 solid"></div>
        <div
            style="width: 895px; height: 0px; left: 895px; top: 88px; position: absolute; transform: rotate(-180deg); transform-origin: 0 0; border: 0.50px #60B669 solid"></div>
        <div
            style="width: 895px; height: 0px; left: 895px; top: 171px; position: absolute; transform: rotate(-180deg); transform-origin: 0 0; border: 0.50px #E8E8E8 solid"></div>
        <div style="width: 795px; height: 205px; left: 64px; top: 22px; position: absolute">
          <div style="width: 784px; height: 43px; left: 0px; top: 0px; position: absolute">
            <div style="width: 107px; height: 43px; left: 0px; top: 0px; position: absolute">
              <div
                  style="left: 0px; top: 24px; position: absolute; color: #999999; font-size: 16px; font-family: Roboto; font-weight: 900; word-wrap: break-word">
                Current Period
              </div>
              <div
                  style="left: 0px; top: 0px; position: absolute; color: #6D7783; font-size: 16px; font-family: Roboto; font-weight: 900; word-wrap: break-word">
                Period 3<br/></div>
            </div>
            <div style="width: 221px; height: 29px; left: 563px; top: 4px; position: absolute">
              <div style="left: 134px; top: 0px; position: absolute"><span
                  style="color: #60B669; font-size: 25px; font-family: Roboto; font-weight: 900; word-wrap: break-word">1:03:</span><span
                  style="color: #60B669; font-size: 25px; font-family: Roboto; font-weight: 300; word-wrap: break-word">51</span>
              </div>
              <div
                  style="left: 0px; top: 11px; position: absolute; color: #6B7581; font-size: 14px; font-family: Roboto; font-weight: 900; word-wrap: break-word">
                Started 4:00 pm
              </div>
            </div>
          </div>
          <div style="width: 795px; height: 29px; left: 0px; top: 93px; position: absolute">
            <div
                style="left: 0px; top: 5px; position: absolute; color: #6D7783; font-size: 16px; font-family: Roboto; font-weight: 900; word-wrap: break-word">
              Period 2
            </div>
            <div style="width: 232px; height: 29px; left: 563px; top: 0px; position: absolute">
              <div style="left: 145px; top: 0px; position: absolute"><span
                  style="color: #415C73; font-size: 25px; font-family: Roboto; font-weight: 900; word-wrap: break-word">1:00:</span><span
                  style="color: #415C73; font-size: 25px; font-family: Roboto; font-weight: 300; word-wrap: break-word">01</span>
              </div>
              <div
                  style="left: 0px; top: 11px; position: absolute; color: #6B7581; font-size: 14px; font-family: Roboto; font-weight: 900; word-wrap: break-word">
                12:09 - 12:09 pm
              </div>
            </div>
          </div>
          <div style="width: 795px; height: 29px; left: 0px; top: 176px; position: absolute">
            <div
                style="left: 0px; top: 5px; position: absolute; color: #6D7783; font-size: 16px; font-family: Roboto; font-weight: 900; word-wrap: break-word">
              Period 1
            </div>
            <div style="width: 229px; height: 29px; left: 566px; top: 0px; position: absolute">
              <div style="left: 142px; top: 0px; position: absolute"><span
                  style="color: #415C73; font-size: 25px; font-family: Roboto; font-weight: 900; word-wrap: break-word">1:23:</span><span
                  style="color: #415C73; font-size: 25px; font-family: Roboto; font-weight: 300; word-wrap: break-word">51</span>
              </div>
              <div
                  style="left: 0px; top: 11px; position: absolute; color: #6B7581; font-size: 14px; font-family: Roboto; font-weight: 900; word-wrap: break-word">
                10:45 - 12:09 pm
              </div>
            </div>
          </div>
        </div>
      </div>
<!--      TOTAL-->
      <div style="width: 185px; height: 29px; left: 665px; top: 486px; position: absolute">
        <div style="left: 98px; top: 0px; position: absolute"><span
            style="color: #60B669; font-size: 25px; font-family: Roboto; font-weight: 900; word-wrap: break-word">3:27:</span><span
            style="color: #60B669; font-size: 25px; font-family: Roboto; font-weight: 300; word-wrap: break-word">42</span>
        </div>
        <div
            style="left: 0px; top: 0px; position: absolute; color: #6A7480; font-size: 25px; font-family: Roboto; font-weight: 900; word-wrap: break-word">
          Total
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {ref} from 'vue';

export default {
  data() {
    return {
      currentTime: 0,
      recordedTimes: [],
      timerInterval: null
    };
  },
  methods: {
    startTimer() {
      this.timerInterval = setInterval(() => {
        this.currentTime++;
      }, 1000);
    },
    stopTimer() {
      clearInterval(this.timerInterval);
      const endTime = new Date().toLocaleTimeString();
      this.recordedTimes.push({
        startTime: this.recordedTimes.length + 1,
        endTime: endTime,
        period: this.currentTime
      });
      this.currentTime = 0;
    },
    formatTime(seconds) {
      const minutes = Math.floor(seconds / 60);
      const remainingSeconds = seconds % 60;
      return `${minutes}:${remainingSeconds < 10 ? '0' : ''}${remainingSeconds}`;
    }
  },
  computed: {
    currentDate() {
      return new Date().toDateString();
    },
    formattedPeriod() {
      return this.formatTime(this.currentTime);
    },
    totalPeriod() {
      return this.recordedTimes.reduce((total, record) => total + record.period, 0);
    }
  }
};
</script>

<style lang="css">
@import './assets/style.css';
</style>
