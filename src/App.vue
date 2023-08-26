<template>
  <div id="app" style=" margin: 0; padding: 0;">

    <!--        date de maintenant-->

    <div
        style="left: 0px; top: 0px; position: absolute; color: #415C73; font-size: 30px; font-family: Roboto; font-weight: 900; word-wrap: break-word">
      Today
      {{ currentDate }}
    </div>
    <!--        stop button-->

    <div
        style="width: 86px; height: 38px; left: 552px; top: 2px; position: absolute; display: flex; align-items: center; justify-content: center; border-radius: 5px; border: 0.50px #CC5252 solid">
      <div class="button stop-button" @click="stopTimer" style="background: none; color: #CC5252;">
        Stop
      </div>
    </div>
  </div>

  <!--        start button-->
  <div
      style="width: 126px; height: 38px; left: 651px; top: 3px; position: absolute; display: flex; align-items: center; justify-content: center; border-radius: 5px; border: 0.50px #60B669 solid">
    <div class="button start-button" @click="startTimer" style="background: none;color:#60B669;">
      Start Now
    </div>
  </div>
  <!--      timer-->
  <div style="left: 809px; top: 8px; position: absolute"><span
      style="color: #60B669; font-size: 25px; font-family: Roboto; font-weight: 900; word-wrap: break-word">{{
      formattedPeriod
    }}</span></div>
  <!--      début du tableau-->
  <div class="table-container">
    <table class="table">
      <tr v-for="(record, index) in sortedRecordedTimes" :key="index">
        <td class="inner">
          <div class="period">Period {{ record.id }}</div>
        </td>
        <td>
          <div class="description" style="text-align: right;">{{ record.endTime }}</div>
        </td>
        <td class="inner" style="text-align: right;">
          <div class="time green">{{ formatTime(record.period) }}</div>
        </td>

        <td style="border: none;"></td>
      </tr>

      <tr>
        <td></td>
        <td style="  color: #6A7480; font-size: 25px; font-family: Roboto; font-weight: 900; word-wrap: break-word; text-align: right">
          Total
        </td>

        <td style="color: #60B669; font-size: 25px; font-family: Roboto; font-weight: 900; word-wrap: break-word;text-align: right">
          {{ formatTime(totalPeriod) }}
        </td>

      </tr>
    </table>
  </div><!--      TOTAL-->


</template>
<script>
import {ref} from 'vue';

export default {
  data() {
    return {
      currentTime: 0,
      recordedTimes: [],
      timerInterval: null,
      isRecording: false, // Nouvelle propriété pour éviter les actions multiples
      nextId: 1 // Initial ID

    };
  },
  methods: {
    startTimer() {
      if (!this.isRecording) {
        this.isRecording = true;
        this.timerInterval = setInterval(() => {
          this.currentTime++;
        }, 1000);
      }
    },
    stopTimer() {
      if (this.isRecording) {
        this.isRecording = false;
        clearInterval(this.timerInterval);

        const startTime = new Date();
        const endTime = new Date();
        endTime.setSeconds(endTime.getSeconds() - this.currentTime);

        const formattedStartTime = startTime.toLocaleTimeString([], {hour: '2-digit', minute: '2-digit'});
        const formattedEndTime = endTime.toLocaleTimeString([], {hour: '2-digit', minute: '2-digit'});

        this.recordedTimes.push({
          id: this.nextId,
          startTime: formattedStartTime,
          endTime: `${formattedStartTime}-${formattedEndTime}`,
          period: this.currentTime
        });

        this.nextId++; // Augmenter l'ID pour le prochain enregistrement
        this.currentTime = 0;
      }
    },
    formatTime(seconds) {
      const minutes = Math.floor(seconds / 60);
      const remainingSeconds = seconds % 60;
      return `${minutes}:${remainingSeconds < 10 ? '0' : ''}${remainingSeconds}`;
    }
  },
  computed: {
    sortedRecordedTimes() {
      // Tri du plus récent au plus ancien
      return this.recordedTimes.slice().sort((a, b) => b.id - a.id);
    },
    currentDate() {
      const date = new Date();
      const day = date.getDate().toString().padStart(2, '0');
      const month = date.toLocaleString('default', {month: 'short'});
      return `${day} ${month}`;
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
