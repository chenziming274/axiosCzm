<template>
  <div>
    中断请求
    <button @click="send">发送请求</button>
    <button @click="off">中断请求</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "abort",
  methods: {
    // axios对xhr.abort()进行二次封装,进行中断请求
    send() {
      const { CancelToken, isCancel } = axios;
      axios({
        method: "GET",
        url: "http://127.0.0.1:5000/server",
        cancelToken: new CancelToken((start) => {
          this.close = start;
        }),
      }).then(
        (response) => {
          console.log("响应成功", response.data);
        },
        (error) => {
          if (isCancel(error)) {
            console.log("中断请求");
          } else {
            console.log("响应失败", error.message);
          }
        }
      );
    },
    off() {
      this.close();
    },
  },
};
</script>

<style>
</style>