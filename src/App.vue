<template lang="pug">
  #app
    header
      span Offline Masonry Gallery
    main
      .wrapper
        .cards
          card(v-for='collection in collections', :key='collection.imageId', :collection='collection')
</template>

<script>
  import cloudinary from 'cloudinary-core'
  import data from './db.json'

  import Card from './components/Card'

  export default {
    name: 'app',
    components: { Card },
    data () {
      return {
        cloudinary: null,
        collections: []
      }
    },
    methods: {
      transform (collection) {
        const imageUrl = this.cloudinary.url(collection.imageId, {
          width: 300,
          crop: 'fit',
          quality: 'auto',
          secure: true
        })
        return Object.assign(collection, { imageUrl })
      }
    },
    created: function () {
      this.cloudinary = cloudinary.Cloudinary.new({
        cloud_name: 'christekh'
      })
      this.collections = data.map(this.transform)
    }
  }
</script>

<style lang="scss">
body {
  margin: 0;
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
  }
  main {
    text-align: center;
    margin-top: 40px;
  }
  header {
    margin: 0;
    height: 56px;
    padding: 0 16px 0 24px;
    background-color: aliceblue;
    span {
      display: block;
      position: relative;
      font-size: 20px;
      line-height: 1;
      letter-spacing: .02em;
      font-weight: 400;
      box-sizing: border-box;
      padding-top: 16px;
    }
  }
  @media only screen and (min-width: 500px) {
    .cards {
      column-count: 2;
    }
  }

  @media only screen and (min-width: 700px) {
    .cards {
      column-count: 3;
    }
  }

  @media only screen and (min-width: 900px) {
    .cards {
      column-count: 4;
    }
  }

  @media only screen and (min-width: 1100px) {
    .cards {
      column-count: 5;
    }
  }
}
</style>
