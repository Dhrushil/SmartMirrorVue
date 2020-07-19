<template>
  <div>
    <v-app style="background-color: #000">
      <Time />
      <DateValue />
      <NewsFeed />
      <Weather />
    </v-app>
  </div>
</template>

<script>
import Time from '@/components/Time.vue'
import DateValue from '@/components/DateValue.vue'
import NewsFeed from '@/components/NewsFeed.vue'
import Weather from '@/components/Weather.vue'


export default {
  components: {
    Time,
    DateValue,
    NewsFeed,
    Weather,

  }
};
</script>

<style>
@font-face {
  font-family: "Product Sans";
  font-style: normal;
  font-weight: 700;
  src: local("Open Sans"), local("OpenSans"),
    url(https://fonts.gstatic.com/s/productsans/v5/HYvgU2fE2nRJvZ5JFAumwegdm0LZdjqr5-oayXSOefg.woff2)
      format("woff2");
}

* {
  text-transform: none !important;
  letter-spacing: 0.04em;
  font-family: Product Sans;
  color: white;
}

.bottom-right {
  position:absolute; 
  right: 0;
  bottom: 0
}

.bottom-left {
  position:absolute; 
  left: 0;
  bottom: 0
}

.top-right {
  position:absolute; 
  right: 0;
  top: 0
}

.top-left {
  position:absolute; 
  left: 0;
  top: 0
}
</style>