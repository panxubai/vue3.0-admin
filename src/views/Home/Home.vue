<template>
  <div class="home">
    <img alt="Vue logo" src="../../assets/logo.png" />
    <button @click="btn">异步axync</button>
  </div>
</template>

<script>
// @ is an alias to /src
import { reactive } from "vue";
export default {
  name: "Home",
  setup() {
    const data = reactive({});
    function btns() {
      return new Promise(resolve => {
        let sino = parseInt(Math.random() * 6 + 1);
        setTimeout(() => {
          resolve(sino);
        }, 3000);
      });
    }
    async function btn() {
      let a = await btns();
      console.log(a);
      console.log(231);
    }
    return {
      data,
      btn
    };
  }
};
</script>
