<template>
  <div class="home">

  </div>
</template>

<script>
// 用于取消正在进行的http请求（了解）

import axios from 'axios'
export default {
  name: 'axios3-6',
  components: {

  },
  created () {
    const source = axios.CancelToken.source()
    axios.get('/data.json', {
      cancelToken: source.token
    }).then(res => {
      console.log(res)
    }).catch(err => {
      console.log(err)
    })

    // 取消请求(message可选，最终被catch捕获)
    source.cancel('cancel http')
  }
}
</script>
