<template lang = 'pug'>
  .container
    .house(ref='houses')
      .title 家族
      .items(v-for='(item, index) in houses' :key='index' @click='showHouse(item)')
        .desc
          .intro {{item.intro}}
          .cname {{item.name}}
          .name {{item.cname}}
    .character
      .title 主要人物
      .section
        .items(v-for='(item, index) in characters' :key='index' @click='showCharacter(item)')
          img(:src='item.profile')
          .desc
            .playedBy {{item.playedBy}}
            .cname {{item.name}}
            .name {{item.cname}}
    .city
      .city-titile 维斯特洛
      .items(v-for='(item, index) in cities' :key='index')
        .title {{item.title}}
        .body {{item.body}}
</template>

<style scoped  lang = 'sass' src = '~/static/sass/index.sass'>
</style>

<script>
  import {mapState} from 'vuex'
  export default {
    head () {
      return {
        title: '冰火脸谱'
      }
    },
    computed: {
      ...mapState([
        'houses',
        'characters',
        'cities'
      ])
    },
    methods: {
      showHouse (item) {
        this.$router.push({
          path: '/house',
          query: {
            id: item._id
          }
        })
      },
      showCharacter (item) {
        this.$router.push({
          path: '/characters',
          query: {
            id: item._id
          }
        })
      }     
    },
    beforeCreate () {
        console.log(`beforeCreate`);
        this.$store.dispatch('fetchHouses')
        this.$store.dispatch('fetchCharacters')
        this.$store.dispatch('fetchCities')
      }
  }
</script>
