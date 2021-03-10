<template>
  <v-app>
    <v-app-bar
      app
      color="yellow"
      dark
    >
      <div class="simpsons text-h4 black--text">The Simpsons Quotes</div>
      <v-spacer></v-spacer>

      <v-btn @click="getQuote()">    
        <span class="simpsons mr-2">Get new Quote!</span>
        <v-icon>mdi-chat-outline</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      
      <div class="text-center">
        <div class="simpsons text-center my-6 text-h4 mx-12 px-12">{{ quote.quote }}</div>

        <div class="simpsons text-center my-6 text-h6">- {{ quote.character }}</div>
      </div>

      <v-img
        :src="quote.image"
        max-height="300"
        contain
        class="mt-2"
      ></v-img>

      

    </v-main>
  </v-app>
</template>

<script>
import './fonts.css';

export default {
  name: 'App',

  data: () => ({
    quote: {
      character: '',
      characterDirection: '', // Right or Left
      image: '',
      quote: '',
    }
  }),

  created() {
    this.getQuote();
  },

  methods: {
    getQuote() {
      fetch(`https://simpsons-quotes-api.herokuapp.com/quotes`)
        .then(res => res.json())
        .then(data => {
          this.quote = data[0];
        })
        .catch(err => {
          console.log('ERROR GETTING SIMPSONS QUOTES');
          console.log(err.message)
        });
    }
  }
};
</script>
<style>
.v-application div.simpsons {
  font-family: SimpsonsFont !important;
}
</style>