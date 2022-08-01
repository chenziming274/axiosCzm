<template>
  <div>
    axios进阶
    <button @click="sendGetServer">向5000端口发送请求</button>
    <button @click="sendGetDev">向5050端口发送请求</button>
    <div class="title">axios发送请求</div>
    <!-- 请求拦截器图例 -->
    <div>
      <button @click="request1">切换模型真实模型</button>
      <button @click="request2">切换模型生活模型</button>
      <button @click="response1">切换模型真实模型</button>
      <button @click="response2">切换模型生活模型</button>
    </div>
    <div class="con">
      <div class="one box">{{one}}</div>
      <div class="two box">{{two}}</div>
      <div class="three box">{{three}}</div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "demo",
  data() {
    return {
      a1:"",
      a2:"",
      one:"第一步,读取配置",
      two:"第二步,操作配置信息",
      three:"第三步,请求拦截器"
    }
  },
  created() {
    // 一.defaults配置默认项
    axios.defaults.headers = {a:100}
    axios.defaults.timeout = 2000
    axios.defaults.baseURL = "http://127.0.0.1:5000"
    
    
    // 二.create方法
    // 当前情况是项目中,需要两个默认配置的时候应该怎么做?
    // 复制完成之后，再次通过defaults添加默认配置
    /*
      1.axios.create方法返回一个全新的axois
      2.全新的axios中的配置根据创建时的配置项
      3.全新的axios 有一点不足,其余的属性与方法均与正常的axios完全一致
    */
    this.a1 = axios.create({
      headers:{a:100},
      timeout:2000,
      baseURL:"http://127.0.0.1:5000"
    })
    this.a2 = axios.create({
      headers:{a:100},
      timeout:2000,
      baseURL:"http://127.0.0.1:5050"
    })
  },
  methods: {
    async sendGetServer() {
      const { data } = await this.a1({
        method: "GET",
        url: `/server`,
        params:{a:1}
      });
      console.log(data);
    },
    async sendGetDev() {
      const { data } = await this.a2({
        method: "GET",
        url: `/dev`,
      });
      console.log(data);
    },
    request1() {
      this.one = "第一步,读取配置"
      this.two = "第二步,操作配置信息"
      this.three = "第三步,请求拦截器"
    },
    request2() {
      this.one = "第一步,买机票,选择时间,选择价位,选择目的地"
      this.two = "第二步,工作人员安排飞行"
      this.three = "第三步,安检,检测核酸证明"
    },
    response1() {
      this.one = "返回参数"
      this.two = "处理参数"
      this.three = "响应拦截器"
    },
    response2() {
      this.one = "玩"
      this.two = "安排旅程"
      this.three = "落地安检,检查核酸证明"
    }
  },
};
</script>

<style>
.title {
  transform: translateY(50px);
  margin: 80px auto 0;
  width: 500px;
  height: 20px;
  font-size: 32px;
}
.con {
  transform: translateY(50px);
  border: 1px solid black;
  width: 500px;
  height: 200px;
  margin: 30px auto;
}
.box {
  float: left;
  margin: 50px 0 0 50px;
  border: 1px solid red;
  width: 100px;
  height: 100px;
}
</style>