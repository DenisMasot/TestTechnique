<template>
  <div class="home">

    <h1>News</h1>
    <select class="home--source" v-model="selected">
      <option disabled value="">Please select one source</option>
      <option value="">All sources</option>
      <option v-for="article in datas.articles" :key="article.id">{{article.source.name}}</option>
    </select>

    <section v-on:click="showAll()" :id="index" v-bind:class="{active: article.isActive}" class="md-card md-theme-demo-lightr" v-for="(article, index) in datas.articles" v-if="selected === article.source.name" :key="article.id">

        <md-card-header >
          <img v-if="article.urlToImage !== null" :src="article.urlToImage" :alt="article.title">
          <div class="md-title">{{article.title}}</div>
        </md-card-header>
        <md-card-content>
          {{article.description}}
        </md-card-content>
        <md-card-actions>
          <md-button :href="article.url" target="_blank">see more</md-button>
        </md-card-actions>
      </section>

      <section v-on:click="showAll(index)"   :id="index"  v-bind:class="{active: article.isActive}" class="md-card md-theme-demo-lightr" v-for="(article, index) in datas.articles" v-if="selected === ''" :key="article.id">

        <md-card-header >
          <img v-if="article.urlToImage !== null" :src="article.urlToImage" :alt="article.title">
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
      selected: '',
      isActive: false
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
  },
  methods: {
    showAll: function (index) {
      console.log('active' + index)
      this.isActive = !this.isActive
      if ($('section#' + index).hasClass('active' + index)) {
        $('section#' + index).removeClass('active' + index)
      } else {
        $('section#' + index).addClass('active' + index)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.home {
  h1{
    font-family: 'Roboto', sans-serif;
    font-size: 200px;
    font-weight: 300;
  }
  .home--source{
    display: block;
    margin: 30px auto;
  }
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
      .md-title{
        font-size: 17px;
        letter-spacing: inherit;
        line-height: initial;
        font-weight: 400;
        padding-top: 10px;
        padding-bottom: 10px;
        display: -webkit-inline-box;
      }
    }
    &[class*="active"] .md-card-content,
    &[class*="active"] .md-card-actions{
      display: block;
    }
    .md-card-content, .md-card-actions{
      display: none;
    }
  }
}
</style>
