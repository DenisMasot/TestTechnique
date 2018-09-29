<template>
  <div class="hello">

    <select v-model="selected">
      <option v-for="article in datas.articles" :key="article.id">{{article.source.name}}</option>
    </select>
    <!-- {{datas.articles}}  -->

    <div>Selected: {{ selected }}</div>

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
<style scoped>

</style>
