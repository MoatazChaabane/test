<template>
  <div id="app">
    <div class="current-date">
      Today {{ currentDate }}
    </div>
<!--    bouton stop -->
    <div class="button stop-button" @click="stopTimer">
      <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 16 16" fill="none">
        <rect width="16" height="16" rx="2" fill="#FF6347"/>
      </svg>
      <span style="margin-left: 8px;">Stop</span>
    </div>
<!--    bouton start-->
    <div class="button start-button" @click="startTimer">
      <svg xmlns="http://www.w3.org/2000/svg" width="13" height="16" viewBox="0 0 13 16" fill="none">
        <path d="M3.61417 0.000195251C3.51794 -0.00204298 3.42224 0.0149816 3.33269 0.0502601C3.24314 0.0855385 3.16154 0.138353 3.09269 0.205619C3.02385 0.272886 2.96914 0.353237 2.93179 0.441949C2.89444 0.530661 2.8752 0.626007 2.8752 0.722262C2.8752 0.818516 2.89444 0.91378 2.93179 1.00249C2.96914 1.0912 3.02385 1.17155 3.09269 1.23882C3.16154 1.30609 3.24314 1.3589 3.33269 1.39418C3.42224 1.42946 3.51794 1.44648 3.61417 1.44425H5.77731V2.93203C2.53641 3.2945 0 6.05149 0 9.38648C0 12.9668 2.92339 15.8889 6.50352 15.8889C10.0837 15.8889 13 12.9668 13 9.38648C13 6.04955 10.4657 3.29052 7.22269 2.93061V1.44425H9.38583C9.48206 1.44648 9.57776 1.42946 9.66731 1.39418C9.75686 1.3589 9.83846 1.30609 9.9073 1.23882C9.97615 1.17155 10.0309 1.0912 10.0682 1.00249C10.1056 0.91378 10.1248 0.818516 10.1248 0.722262C10.1248 0.626007 10.1056 0.530661 10.0682 0.441949C10.0309 0.353237 9.97615 0.272886 9.9073 0.205619C9.83846 0.138353 9.75686 0.0855385 9.66731 0.0502601C9.57776 0.0149816 9.48206 -0.00204298 9.38583 0.000195251H3.61417ZM6.50352 4.33368C9.30327 4.33368 11.556 6.58659 11.556 9.38648C11.556 12.1864 9.30327 14.4449 6.50352 14.4449C3.70378 14.4449 1.44538 12.1864 1.44538 9.38648C1.44538 6.58659 3.70378 4.33368 6.50352 4.33368ZM6.49225 5.76648C6.39732 5.76741 6.30351 5.78707 6.21618 5.82429C6.12885 5.86152 6.04972 5.91564 5.98331 5.98349C5.91691 6.05133 5.86453 6.13162 5.82918 6.21973C5.79384 6.30784 5.77621 6.40203 5.77732 6.49696V10.1113C5.7777 10.2062 5.79679 10.3002 5.83351 10.3878C5.87023 10.4753 5.92385 10.5547 5.9913 10.6215C6.05875 10.6883 6.13871 10.7412 6.22661 10.777C6.3145 10.8129 6.40861 10.8311 6.50353 10.8305H8.66668C8.7628 10.8326 8.85837 10.8155 8.94778 10.7801C9.03719 10.7448 9.11864 10.6919 9.18736 10.6246C9.25607 10.5574 9.31067 10.4771 9.34794 10.3884C9.38521 10.2998 9.40441 10.2046 9.40441 10.1085C9.40441 10.0123 9.38521 9.9172 9.34794 9.82857C9.31067 9.73993 9.25607 9.65957 9.18736 9.59232C9.11864 9.52507 9.03719 9.47223 8.94778 9.43688C8.85837 9.40152 8.7628 9.38441 8.66668 9.38648H7.22269V6.49696C7.22381 6.40072 7.20569 6.3052 7.16937 6.21607C7.13306 6.12694 7.0793 6.04604 7.01125 5.97799C6.94319 5.90993 6.86222 5.85611 6.77309 5.8198C6.68396 5.78349 6.58848 5.76536 6.49224 5.76648H6.49225Z" fill="#60B669"/>
      </svg> <span style="margin-left: 8px;"> Start Now </span>
    </div>
<!--timer-->
    <div class="timer">
      {{ formattedPeriod }}
    </div>
    <div class="table-container">
<!--      tableau d'historique-->
      <table class="table">
        <tr v-for="(record, index) in sortedRecordedTimes" :key="index">
          <td class="inner">
            <div class="period">Period {{ record.id }}</div>
          </td>
          <td>
            <div class="description">{{ record.endTime }}</div>
          </td>
          <td class="inner">
            <div class="time green">{{ formatTime(record.period) }}</div>
          </td>
          <td></td>
        </tr>
        <tr>
          <td></td>
          <td class="total-title">Total</td>
          <td class="total-time">{{ formatTime(totalPeriod) }}</td>
        </tr>
      </table>
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
          endTime: `${formattedEndTime}-${formattedStartTime}`,
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
#app {
  font-family: Arial, sans-serif;
  text-align: center;
  padding: 20px;
}
</style>
