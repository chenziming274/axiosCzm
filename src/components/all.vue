<template>
  <div>
    批量发送请求
    <button @click="sendAll">很复杂的业务逻辑,一次发送很多请求</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name:"all",
  methods: {
    async sendAll() {
      // all 方法
      const p1 = axios({
        url:"http://127.0.0.1:5000/server",
        method:"GET",
        params:{a:1}
      })

      const p2 = axios({
        url:"http://127.0.0.1:5000/server",
        method:"GET",
        params:{a:2}
      })

      const p3 = axios({
        url:"http://127.0.0.1:5000/server",
        method:"GET",
        params:{a:3}
      })

      axios.all([p1,p2,p3]).then(
        response => {console.log("三次请求都成功了",response)},
      )

      // 依次执行
      const p1 = await axios({
        url:"http://127.0.0.1:5000/server",
        method:"GET",
        params:{a:1}
      })
      const p2 = await axios({
        url:"http://127.0.0.1:5000/server",
        method:"GET",
        params:{a:1}
      })
      const p3 = await axios({
        url:"http://127.0.0.1:5000/server",
        method:"GET",
        params:{a:1}
      })
      console.log(p1,p2,p3)
    },
  },
}
</script>

<style>

</style>