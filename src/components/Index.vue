<template>
  <q-layout>
    <div slot="header" class="toolbar">
      <q-toolbar-title :padding="0">

      </q-toolbar-title>
    </div>

    <!--
      Replace following "div" with
      "<router-view class="layout-view">" component
      if using subRoutes
    -->
    <div class="layout-view">

        <div class="slider__wrapper">
          <q-gallery-slider  :src="galleryPhotos"></q-gallery-slider>
        </div>
        <!-- <template v-for="photo in fbPhotos" >
          <img :key="photo['.key']" class="responsive image" :src="photo['.value']" alt="">
        </template> -->

    </div>
  </q-layout>
</template>

<script>
var firebase = require('firebase')
var config = {
  apiKey: 'AIzaSyCNIjlw4gVqGQgSr6pvcHqmWK4eA1KnTyk',
  authDomain: 'vue-firebase-e123d.firebaseapp.com',
  databaseURL: 'https://vue-firebase-e123d.firebaseio.com',
  storageBucket: 'vue-firebase-e123d.appspot.com',
  messagingSenderId: '121034532316'
}
var _ = require('lodash')
console.log(_);
var firebaseApp = firebase.initializeApp(config)
const DB = firebaseApp.database()
// const auth = firebase.auth()
const PHOTOS = firebase.storage()
// var usersRef = db.ref('users')
// var postsRef = db.ref('posts')
var photosDBRef = DB.ref('photos')
// var photosRef = photos.ref('folder1');


import { Utils } from 'quasar'

export default {
  data () {
    return {
    }
  },

  firebase: {
    fbPhotos: photosDBRef
  },

  computed: {
    galleryPhotos () {
      // var users = {
      //   'fred':    { 'user': 'fred',    'age': 40 },
      //   'pebbles': { 'user': 'pebbles', 'age': 1 }
      // };
      //
      // _.mapValues(users, function(o) { return o.age; });
      // // => { 'fred': 40, 'pebbles': 1 } (iteration order is not guaranteed)
      //
      // // The `_.property` iteratee shorthand.
      // return _.mapValues(users, 'age');
      // // => { 'fred': 40, 'pebbles': 1 } (iteration order is not guaranteed)
      return _.mapValues(this.fbPhotos, '.value')
    }
  },
  methods: {

  },
  mounted () {

  },
  beforeDestroy () {

  }
}
</script>

<style lang="styl">
.image, video {
  object-fit: cover;
  display: block;
  width: 200px;
  height: 280px !important;
  border: 1px solid;
}

video {
  object-fit: contain;
}

.slider__wrapper {
  max-width: 700px;
}
</style>
