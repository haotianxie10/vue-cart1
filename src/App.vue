<template>
  <div class="app-container">
    <Header></Header>
    <Goods
      v-for="item in list"
      :key="item.id"
      :id="item.id"
      :title="item.goods_name"
      :pic="item.goods_img"
      :price="item.goods_price"
      :state="item.goods_state"
      :count="item.goods_count"
      @state-change="getNewState"
    ></Goods>

    <Footer
      :isfull="fullState"
      @full-change="getFullState"
      :total="total"
      :all="allin"
    ></Footer>
  </div>
</template>

<script>
import Header from "@/components/Header/Header.vue";
import axios from "axios";
import Goods from "@/components/Goods/Goods.vue";
import Footer from "@/components/Footer/Footer.vue";
import bus from "@/eventBus.js";
export default {
  data() {
    return {
      list: [],
    };
  },
  computed: {
    fullState() {
      return this.list.every((item) => item.goods_state);
    },
    total() {
      return this.list
        .filter((item) => item.goods_state)
        .reduce((amt, item) => (amt += item.goods_price * item.goods_count), 0);
    },
    allin() {
      return this.list
        .filter((item) => item.goods_state)
        .reduce((e, item) => (e += item.goods_count), 0);
    },
  },
  created() {
    this.initCartList();
    bus.$on("share", (e) => {
      this.list.some((item) => {
        if (item.id === e.id) {
          item.goods_count = e.value;
          return true;
        }
      });
    });
  },
  methods: {
    async initCartList() {
      const { data: res } = await axios.get("https://www.escook.cn/api/cart");
      if (res.status === 200) {
        this.list = res.list;
      }
    },
    getNewState(e) {
      // console.log(e);
      this.list.some((item) => {
        if (item.id === e.id) {
          item.goods_state = e.value;
          return true;
        }
      });
    },
    getFullState(e) {
      this.list.forEach((item) => (item.goods_state = e));
    },
  },
  components: {
    Header,
    Goods,
    Footer,
  },
};
</script>

<style lang="less" scoped>
.app-container {
  padding-top: 45px;
  padding-bottom: 50px;
}
</style>
