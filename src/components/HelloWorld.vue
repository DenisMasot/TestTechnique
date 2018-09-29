<template>
  <div class="hello">

    <div v-for="data in datas" :key="data.id">{{data}} <br><br></div>

    <hr>
    {{datas.articles}}
  </div>
</template>

<script>

import axios from 'axios'
export default {
  name: 'HelloWorld',
  data () {
    return {
      datas: []
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
