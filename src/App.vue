<template>
  <div class="black-bg" v-if="isOpenedModalPage" @click="clickImg()">
    <div class="white-bg">
      <h4>상세페이지</h4>
      <p>상세페이지 내용임</p>
    </div>
  </div>
  <div class="menu">
    <a v-for="a in 메뉴들" :key="a">{{ a }}</a>
  </div>

  <p>원룸샵</p>
  <div v-for="(name, i) in oneRooms" :key="i">
    <img class="room-img" :src="getImgUrl(i)" @click="clickImg()"/>
    <h4 :style="스타일">{{ name }}</h4>
    <p>{{ (i + 1) * 1000 }} 만원</p>
    <p>{{isOpenedModalPage}}</p>
    <button @click="increase(i)">혀위매물신고</button>
    <span> 신고수 : {{ 신고수[i] }} </span>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      isOpenedModalPage : false,
      신고수: [0, 0, 0],
      메뉴들: ["Home", "Shop", "About"],
      oneRooms: ["역삼동원룸", "천호동원룸", "마포구원룸"],
    };
  },
  methods: {
    increase(i) {
      this.신고수[i] += 1;
    },
    getImgUrl(i) {
      let url = require("./assets/room".concat(String(i)).concat(".jpg"));
      return url;
    },
    clickImg(){
      if(this.isOpenedModalPage){
        this.isOpenedModalPage = false;
      }else{
        this.isOpenedModalPage = true;
      }
    }
  },

  components: {},
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}

body{
  margin: 0;
}

div{
  box-sizing: border-box;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}

.black-bg {
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  background: wheat;
  width :100%; border-radius: 8px;
  padding: 20px;
}
</style>
