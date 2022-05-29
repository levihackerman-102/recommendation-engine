<template>
  <q-page class="flex flex-center">

    <div class="q-pa-md-xl bg-grey-10 text-white instructions">
      <q-list dark bordered separator style="max-width: 500px">
        <q-item clickable v-ripple>
          <q-item-section>Type in your favourite movie</q-item-section>
        </q-item>

        <q-item clickable v-ripple>
          <q-item-section>
            <q-item-label>The search bar will have options popping up</q-item-label>
          </q-item-section>
        </q-item>

        <q-item clickable v-ripple>
          <q-item-section>
            Select your favourite movie option &#38; 'Generate Recommendations!'
          </q-item-section>
        </q-item>
      </q-list>
    </div>

    <div class="search">

      <q-input clearable filled color="purple-12" v-model="movieTitle" label="Enter movie name here" />

      <q-btn class="q-mx-md" push color="primary" label="Generate recommendations" @click="generateRecommendations" />
    
    </div>

    <div class="recommended" v-show="this.isRecommended" v-for="movie in this.recommendations" :key="movie">
      
      <img v-if="movie['poster']=='True'" :src="getImgURL(movie['movieId'])" alt="poster-x">
    
    </div>

    <div v-show="!this.isRecommended" class="error">
      <p color="red"> This movie is not in our database, please try searching for some other movie. </p>
    </div>

  </q-page>
</template>

<script>
import { ref } from 'vue'
import axios from 'axios';
import all_movies_json from '../assets/json/movies.json';
import $ from 'jquery';

export default ({
   setup () {
    return {
      text: ref(),
      controlType: ref('flat') 
    }
  },

  data() {
    return {
      movieTitle: '',
      api_recommendations: [],
      recommendations: [],
      isRecommended: true,
      movie: {}
    };
  },

  methods: {
    generateRecommendations: function() {
      // var self = this;
      // axios.post('http://0.0.0.0:8081/recms', {
      //   movie_title: self.movieTitle
      // })
      // .then(function(response){
      //   self.recommendations = response.data.rec_movie                           //api_recommendations is an array containing a list of titles
      //   isRecommended = true
      // })
      var self = this;
      self.recommendations = [];
      axios.post('http://0.0.0.0:8081/recms', {
        movie_title: this.movieTitle
      })
      .then(function(response){
        var api_recommendations = response.data.rec_movie                           // api_recommendations is an array containing a list of titles
        if(api_recommendations[0] === "Movie not found") {
          self.isRecommended = false
          return
        }
        self.isRecommended = true
        var found_movie = [];                                                       // dummy variable to store a matched movie
        
        $.each(api_recommendations,function(movie_title){                           // movie_title is just an index 0,1,2..
                    
            found_movie = all_movies_json.filter((obj) => obj.title === api_recommendations[movie_title]);
            self.recommendations.push(found_movie[0])
        });
        self.recommendations = self.recommendations.slice(0,Math.min(self.recommendations.length,5))
        // console.log(self.recommendations)
      })
    },
    getImgURL: function(id) {
      return `https://raw.githubusercontent.com/levihackerman-102/posters/master/posters/${id}.jpg`
    }
  }
})

</script>

<style>
  .instructions {
    position: absolute;
    top: 5rem;
    border: 3px solid green;
    font-size: 1.3rem;
  }

  .q-input {
    margin-top: -4.1rem;
  }

  .q-btn {
    margin-top: 1.5rem;
  }

  .search {
    position: absolute;
    left: 49rem;
  }

  .recommended {
    display: flex;
    justify-content: space-evenly;
    position: relative;
    left: -0.5rem;
    top: 14rem;
  }

  .recommended img {
    margin: 0 1rem 0 1rem;
  }

  .error {
    position: absolute;
    top: 35rem;
    background-color: blanchedalmond;
  }

  .error p {
    color: red;
    font-size: 1.5rem;
  }

</style>
