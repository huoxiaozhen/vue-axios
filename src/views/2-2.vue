<template>
  <div class="home">

  </div>
</template>

<script>
/* axios请求方法： get,post,put,patch,delete

  get: 获取数据
  post: 提交数据(表单提交+文件上传)
  put: 更新数据(所有数据推送到后端)
  patch: 更新数据(只将修改的数据推送到后端)
  delete: 删除数据

*/
import axios from 'axios'
export default {
  name: 'axios2-2',
  components: {

  },
  created () {
    axios.get('/data.json', {
      params: {
        id: 12
      }
    }).then((res) => {
      console.log(res)
    })
    axios({
      method: 'get',
      url: '/data.json',
      params: {
        id: 12
      }
    }).then((res) => {
      console.log(res)
    })
    // post
    // form-data 表单提交 (图片上传，文件上传)
    // applicition/json
    const data = {
      id: 12
    }
    axios.post('/post', data).then((res) => {
      console.log(res)
    })
    axios({
      method: 'post',
      url: '/post',
      data: data
    }).then((res) => {
      console.log(res)
    })
    // form-data 请求
    const formData = new FormData()
    for (const key in data) {
      formData.append(key, data[key])
    }
    axios.post('/post', formData).then((res) => {
      console.log(res)
    })
  }
}
</script>
