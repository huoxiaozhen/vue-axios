<template>
  <div class="home">

  </div>
</template>

<script>
// 错误处理： 请求错误时进行的处理

import axios from 'axios'
export default {
  name: 'axios3-5',
  components: {

  },
  created () {
    // 例子：实际开发过程中，一般添加统一的错误处理
    let instance = axios.create()
    instance.interceptors.request.use(config => {
      return config
    }, err => {
      // 请求错误 一般http状态码以4开头，常见：401超时， 404 not found
      $('#model').show()
      setTimeout(() => {
        $('#model').hide()
      }, 2000)
      return Promise.reject(err)
    })

    instance.interceptors.response.use(res => {
      return res
    }, err => {
      // 响应错误处理 一般http状态码以5开头，常见：500系统错误， 502系统重启
      $('#model').show()
      setTimeout(() => {
        $('#model').hide()
      }, 2000)
      return Promise.reject(err)
    })

    instance.get('/data.json').then(res => {
      console.log(res)
    }).catch(err => {
      console.log(err)
    })
  }
}
</script>
