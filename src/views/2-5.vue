<template>
  <div class="home">axios并发请求</div>
</template>

<script>
// 并发请求：同时进行多个请求，并统一处理
import axios from 'axios'

export default {
  name: 'axios2-5',
  components: {},
  created () {
    // axios.all() axios.spread()
    axios.all([
      axios.get('/data.json'),
      axios.get('/city.json')
    ]).then(
      axios.spread((dataRes, cityRes) => {
        console.log(dataRes, cityRes)
      })
    )
  }
}
</script>
