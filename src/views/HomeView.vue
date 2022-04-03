<template>
  <div class="home">
    <div class="square-container">
      <div class="square-container-innner">
        <div class="first-line">
          <div><span>{{ dicObj.query }}</span></div>
          <div @click="handlePlayAudio"><img src="@/assets/laba.png" alt="laba"></div>
          <div><img src="@/assets/love-inactive.png" alt="laba"></div>
        </div>
        <div class="second-line">
          <p v-for="item in dicObj.basic.explains" :key="item.id">{{ item }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "HomeView",
  components: {},
  data() {
    return {dicObj: {basic: {explains: ""}}};
  },
  methods: {
    handlePlayAudio() {
      let audio = new Audio(this.dicObj.speakUrl);
      audio.play();
    }
  },
  mounted() {
    parent.postMessage({type: "iframe2ext", data: {result: "", status: "mounted"}}, "*");
    window.addEventListener("message", (e) => {
      if (e.data.type == "ext2iframe") {
        console.log(e.data);
        this.dicObj = e.data.result;
      }
    });
  }
};
</script>

<style lang="less">
.square-container {
  font-size: 15px;
  width: 300px;
  padding: 2px;
  border-radius: 3px;
  box-sizing: border-box;
  position: fixed;
  background-color: white;
  z-index: 999;
}

.square-container-innner {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  /*align-items: center;*/
}

.first-line {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;
}

.first-line > div:nth-child(2) > img {
  height: 20px;
  margin-left: 10px;
  cursor: pointer;
}

.first-line > div:nth-child(3) > img {
  height: 20px;
  margin-left: 10px;
  cursor: pointer;
}


.second-line {
  font-size: 12px;
}

</style>