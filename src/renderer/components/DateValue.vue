<template>
<div>
    <h3 style="font-size: 200%;">{{text}}</h3>
</div>
</template>

<script>
export default {
    data: () => ({
    text: ""
  }),
  methods: {
    startDate() {
      var date = new Date();
      var day = date.getDay();
      var theDate = date.getDate();
      var month = date.getMonth();

      day = this.checkDay(day);
      theDate = this.checkOrdinal(theDate);
      month = this.checkMonth(month);

      this.text = day + " " + theDate + " " + month;
      setTimeout(this.startDate, 500)
    },

    checkDay(val) {
        switch (val) {
        case 0:
          val = "Sunday";
          return val;
          break;
        case 1:
          val = "Monday";
          return val;
          break;
        case 2:
          val = "Tuesday";
          return val;
          break;
        case 3:
          val = "Wednesday";
          return val;
          break;
        case 4:
          val = "Thursday";
          return val;
          break;
        case 5:
          val = "Friday";
          return val;
          break;
        case 6:
          val = "Saturday";
          return val;
      }
    },

    checkMonth(val) {
        switch (val) {
        case 0:
          val = "January";
          return val;
        case 1:
          val = "February";
          return val;
        case 2:
          val = "March";
          return val;
        case 3:
          val = "April";
          return val;
        case 4:
          val = "May";
          return val;
        case 5:
          val = "June";
          return val;
        case 6:
          val = "July";
          return val;
        case 7:
          val = "August";
          return val;
        case 8:
          val = "September";
          return val;
        case 9:
          val = "October";
          return val;
        case 10:
          val = "November";
          return val;
        case 11:
          val = "December";
          return val;
      }
    },

    checkOrdinal(val) {
        if (val > 3 && val < 21) {
        val = val + "th";
        return val;
      }
      switch (val % 10) {
        case 1:
          val = val + "st";
          return val;
        case 2:
          val = val + "nd";
          return val;
        case 3:
          val = val + "rd";
          return val;
        default:
          val = val + "th";
          return val;
      }
    }
  },
  mounted() {
      this.startDate();
  }
}
</script>