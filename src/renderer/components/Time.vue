<template>
    <div class="time">
      <h1 style="font-size: 700%">{{time}}</h1>
    </div>
</template>

<script>
export default {
  data: () => ({
    time: ""
  }),
  methods: {
    startTime() {
      var date = new Date();
      var hours = date.getHours();
      var minutes = date.getMinutes();
      var seconds = date.getSeconds();

      minutes = this.checkTime(minutes);
      seconds = this.checkTime(seconds);

      this.time = hours + ":" + minutes + ":" + seconds;
      setTimeout(this.startTime, 500);
    },

    checkTime(val) {
      if (val < 10) {
        val = "0" + val;
      }
      return val;
    }
  },

  mounted() {
      this.startTime();
  }
};
</script>