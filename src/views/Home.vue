<template>
  <div class="home" id="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <div ref="message" class="message">{{ message }}</div>
    <input type="text" placeholder="請輸入" v-model="message" />
    <br />
    <button type="button" @click="time()">觸發時間(五秒)</button>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  data() {
    return {
      message: "這裡是一個字串資料",
      num: 0,
      timer: null,
    };
  },
  computed: {
    changeNum() {
      return this.num + 1;
    },
  },
  methods: {
    time() {
      this.timer = setTimeout(() => {
        alert("時間倒數結束");
      }, 5000);
    },
  },
  beforeCreate() {
    console.log("--------------beforeCreate-------------");
    console.log("message: " + this.message); // undefined
    console.log("computed: " + this.changeNum); // undefined
    console.log("about Dom: " + this.$refs.message); // undefined
    console.log("--------------beforeCreate-------------");
  },
  created() {
    console.log("--------------created-------------");
    console.log("message: " + this.message); // 這裡是一個字串資料
    console.log("computed: " + this.changeNum); // 1
    console.log("about Dom: " + this.$refs.message); // undefined
    console.log("--------------created-------------");
  },
  beforeMount() {
    console.log("--------------beforeMount-------------");
    console.log("message: " + this.message); // 這裡是一個字串資料
    console.log("computed: " + this.changeNum); // 1
    console.log("about Dom: " + this.$refs.message); // undefined
    // 這個階段似乎跟 Vue2 不太一樣 ?
    console.log("--------------beforeMount-------------");
  },
  mounted() {
    console.log("--------------mounted-------------");
    console.log("message: " + this.message); // 這裡是一個字串資料
    console.log("computed: " + this.changeNum); // 1
    console.log("about Dom: " + this.$refs.message); // [object HTMLDivElement]
    console.log(document.querySelector(".message"));
    console.log("--------------mounted-------------");
  },
  beforeUpdate() {
    // input v-model TEST
    console.log("--------------beforeUpdate-------------");
    console.log("狀態已經更新");
    console.log("--------------beforeUpdate-------------");
  },
  updated() {
    // input v-model TEST
    console.log("--------------updated-------------");
    console.log("狀態跟畫面都已經更新");
    console.log("--------------updated-------------");
  },
  beforeUnmount() {
    // 切換到其他路由 TEST
    console.log("--------------beforeUnmount-------------");
    alert("Vue 的實體被銷毀前");
    console.log("Vue 的實體被銷毀前");
    console.log("--------------beforeUnmount-------------");
  },
  unmounted() {
    // 切換到其他路由 TEST
    console.log("--------------unmounted-------------");
    alert("Vue 的實體已被銷毀，無法再做任何事情");
    console.log("Vue 的實體已被銷毀，無法再做任何事情");
    clearTimeout(this.timer); // 銷毀前記得清除 setTimeout
    console.log("--------------unmounted-------------");
  },
};
</script>
