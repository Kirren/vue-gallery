<template lang="pug">
  .card
    img.card-img-top(:src='collection.imageUrl', :alt='collection.collector')
    i.fa.fa-heart.fa-5x(@click="")
    .card-body
      h4.card-title {{ collection.collector }}
      p.card-text {{ collection.description }}
</template>

<script>
  export default {
    props: ['collection'],
    name: 'card'
  }
</script>

<style lang="scss">
  .card {
    position: relative;
    display: inline-block;
    margin-bottom: 1rem;
    border-color: transparent;
    background-color: aliceblue;
    opacity: .7;
    &:hover, &:focus {
      cursor: pointer;
      background-color: blanchedalmond;
      opacity: 1;
      transition: all .7s ease-in-out;
      i.fa-heart {
        opacity: 1;
        text-shadow: 0 0 2rem #7d7d7d;
        transition: opacity .1s ease-in-out;
      }
    }
    i.fa-heart {
      position: absolute;
      opacity: 0;
      color: #fff;
      top: 30px;
      bottom: 0;
      left: 0;
      right: 0;
    }
  }
</style>
