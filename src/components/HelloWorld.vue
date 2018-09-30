<template>
  <div class="home">

    <select v-model="selected">
      <option disabled value="">Please select one</option>
      <option v-for="article in datas.articles" :key="article.id">{{article.source.name}}</option>
    </select>

        <section class="md-card md-theme-demo-lightr" v-for="article in datas.articles" v-if="article.source.name === selected" :key="article.id">
          <md-card-header >
            <img :src="article.urlToImage" :alt="article.title">
            <div class="md-title">{{article.title}}</div>
          </md-card-header>

          <md-card-content>
            {{article.description}}
          </md-card-content>

          <md-card-actions>
            <md-button :href="article.url" target="_blank">see more</md-button>
          </md-card-actions>
        </section>
  </div>
</template>

<script>

import axios from 'axios'
export default {
  name: 'HelloWorld',
  data () {
    return {
      datas: [],
      selected: ''
    }
  },
  created () {
    var vm = this
    axios.get('https://newsapi.org/v2/top-headlines?country=us&apiKey=58974f437ca74c9b9ba330148e3403e3')
      .then(function (response) {
        vm.datas = response.data
      })
      .catch(error => {
        console.log(error.response)
      })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.home {
    .md-card {
      width: 320px;
      margin: 4px;
      display: inline-block;
      vertical-align: top;
      .md-card-header{
        padding: 0;
        &>img {
          border-radius: 0;
        }
      }
      .md-card-content, .md-card-actions{
        display: none;
      }
    }
}
</style>
