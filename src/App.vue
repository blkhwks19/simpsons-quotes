<template>
  <v-app>
    <v-app-bar
      app
      color="yellow"
      
    >
      <div class="simpsons text-md-h4 text-sm-h6 text-body-1">The Simpsons Quotes</div>
      <v-spacer></v-spacer>

      <v-btn color="pink" dark @click="getQuote()">    
        <span class="simpsons mr-2">Get new Quote!</span>
        <v-icon>mdi-chat-outline</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main class="mb-12">

      <div v-if="loading" class="text-center mt-12">
        <v-progress-circular
          indeterminate
          :size="50"
          :width="7"
          color="pink"
        ></v-progress-circular>
      </div>

      <div v-else>
      
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

      </div>

    </v-main>
  </v-app>
</template>

<script>
import './fonts.css';

export default {
  name: 'App',

  data: () => ({
    loading: false,
    quote: {
      character: '',
      characterDirection: '', // Right | Left
      image: '',
      quote: '',
    }
  }),

  created() {
    this.getQuote();
  },

  methods: {
    getQuote() {
      this.loading = true;
      fetch(`https://simpsons-quotes-api.herokuapp.com/quotes`)
        .then(res => res.json())
        .then(data => {
          this.quote = data[0];
          this.loading = false;
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