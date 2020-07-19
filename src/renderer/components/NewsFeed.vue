<template>
<div style="position: absolute; bottom: 10em; text-align: center; width: 50%">
      <p style="padding-bottom: 0.5em; font-size: 2em">{{newsTitle}}</p>
      <p>{{newsDescription}}</p>
      <div style="width:50%; left: 25%; position: relative; padding-top:0.5em">
      <v-img contain :src="`${newsImage}`"></v-img>
      <v-btn outlined fab color="white" style="float:left" @click="checkNews(changeNews--)"><v-icon>fa-backward</v-icon></v-btn> 
      <v-btn outlined fab color="white" style="float: right" @click="checkNews(changeNews++)"><v-icon>fa-forward</v-icon> </v-btn>
      </div>
    </div>
</template>

<script>
export default {
  data: () => ({
    newsTitle: null,
    newsDescription: null,
    newsImage: null,
    changeNews: 0,
  }),

  methods: {
    newsStartup() {
      var date = new Date();
      var minutes = date.getMinutes();
      var seconds = date.getSeconds();
      if (minutes % 5 == 0 && seconds == 0) {
        this.checkNews(Math.floor(Math.random() * 10));
      }
      if (this.changeNews > 9) {
      this.changeNews = 0
    }else if (this.changeNews < 0) {
      this.changeNews = 9
    }
      setTimeout(this.newsStartup, 1000);
    },
    checkNews(articleId) {
      let self = this;
      var url =
        "http://newsapi.org/v2/top-headlines?" +
        "sources=bbc-news&" +
        "apiKey=666b8340d8e243ba8c0fd5bad09cdf8b";
      var req = new Request(url);
      fetch(req)
        .then(response => response.json())
        .then(({ articles }) => {
          console.log(articles);
          self.newsTitle = articles[articleId].title;
          self.newsDescription = articles[articleId].description;
          self.newsImage = articles[articleId].urlToImage;
        });
    }
  },
  mounted() {
   this.newsStartup();
    this.checkNews(Math.floor(Math.random() * 10));
    
    
  }
};
</script>
