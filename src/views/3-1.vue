<template>
  <div class="home"></div>
</template>

<script>
// axios实例
import axios from 'axios'

export default {
  name: 'axios3-1',
  components: {},
  created () {
    const instance = axios.create({
      baseUrl: 'http://localhost:8080',
      timeout: 1000
    })
    instance.get('/data.json').then(res => {
      console.log(res)
    })
  }
}
</script>
