<template>
  <div>
    <div class="bar" ref="bar"></div>
    <div class="footer">
      拦截器
      <button @click="sendGetServer">点击发送请求 测试拦截器参数</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "interceptors",

  created() {
    // 配置请求拦截器
    // 当前为货架页面,参数传递的是货物的价格 货物当前显示的都是美元
    // 后端只接受换算成RMB,
    /*
      axios请求拦截器
      1.本质就是一个函数
      2.请求发送之前会调用请求拦截器函数,并传入本次请求全部配置信息
      3.请求拦截器一定要返回配置信息,要不然永远无法发送请求
      4.用于对请求的各种配置进行修改,甚至取消本次请求
    */
    axios.interceptors.request.use((config) => {
      this.start()
      return config
    })
    // 响应拦截器有两个参数,分别对成功与失败进行处理
    axios.interceptors.response.use(
      // 他是对axios底层依然是对 xhr.readyState === 4 以及 对 xhr.status 是否以2开头进行判断
      (response)=>{
        console.log(response.data,"响应成功了")
        this.stop()
        return response.data
      },
      error => {
        this.stop()
        console.log(error)
      }
    )
  },
  methods: {
    sendGetServer() {
      axios({
        method: "GET",
        url: `http://127.0.0.1:5000/server`,
        params: { price: 100 },
      }).then((response) => console.log("请求成功了",response));
    },
    start() {
      this.$nextTick(() => {
        this.$refs.bar.style.cssText = "width:990px";
      });
    },
    stop() {
      setTimeout(() => {
        this.$nextTick(() => {
          this.$refs.bar.style.cssText = "display: none;";
        });
      }, 2000);
    },
  },
};
</script>

<style>
.bar {
  width: 1px;
  height: 5px;
  background-color: skyblue;
  transition: width 2s;
}
.footer {
  margin-top: 20px;
}
</style>