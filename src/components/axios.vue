<template>
  <div class="hello">
    axios介绍
    <button @click="sendGET">点击发送get请求</button>
    <button @click="sendGetByQuery">点击发送get请求,携带query参数</button>
    <button @click="sendByBody">点击发送请求,携带请求体参数</button>
    <button @click="sendDelete">点击发送DELETE请求</button>
  </div>
</template>

<script>
import axios from "axios"
export default {
  name: 'HelloWorld',
  data() {
    return {
      id:"123",
    }
  },
  methods: {
    // axios 发送get请求 不携带参数
    async sendGET() {
      // 最完整写法, 
      axios({
        method:"get",
        url:"http://127.0.0.1/server",
        headers:{
          a:100
        }
      }).then(response => {
        console.log(response.data,"请求成功了")
      })

      // 精简写法
      // const {data} = await axios.get("http://127.0.0.1/server")
      console.log(data)
    },
    // axios 发送任何请求 携带query参数
    async sendGetByQuery() {
      // 完整写法
      // const {data} = await axios({
      //   method:"GET",
      //   url:"http://127.0.0.1/server",
      //   params:{
      //     id:"123",
      //     name:"陈子铭"
      //   }
      // })
      // console.log(data)

      // 简写方式
      const {data} = await axios.get("http://127.0.0.1/server",{params:{id:"123",name:"陈子铭"}})
      console.log(data)
    },
    async sendByBody() {
      // 完整写法
      // const {data} = await axios({
      //   method:"post",
      //   url:"http://127.0.0.1/server",
      //   // data:"id=123&name=陈子铭"
      //   data:{
      //     id:"123",
      //     name:"陈子铭"
      //   }
      // })
      // 当我发送请求的时候,携带请求体参数,默认采用JSON格式,并且自动配置请求头
      // 当我发送请求的时候,携带请求体参数 参数定义为字符串,他会作为urlencoded进行解析,并且自动配置请求头
      // const {data} = await axios.post("http://127.0.0.1/server",{id:"123",name:"陈子铭"})
      // 注意 如果简写的话不能添加 key 
      console.log(data)
      let per = {
        id:"123",
        name:"陈子铭"
      }
      const {data} = await axios.post("http://127.0.0.1/server",per)
    },
    async sendDelete() {
      // 完整写法
      const {data} = await axios({
        method:"delete",
        url:`http://127.0.0.1/server/${this.id}`,
      })
      console.log(data)
    },
    // 

    async abc() {
      // 完整写法
      const {data} = await axios({
        method:"delete",
        url:`/server/${this.id}`,
        baseURL:"http://127.0.0.1", // 基础路径配置,
        headers:{
          a:100
        },
        timeout:2000
      })
      console.log(data)
    },
  },
}
</script>

<style scoped>
</style>
