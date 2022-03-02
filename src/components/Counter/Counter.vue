<template>
  <div
    class="number-container d-flex justify-content-center align-items-center"
  >
    <!-- 减 1 的按钮 -->
    <button type="button" class="btn btn-light btn-sm" @click="minus">-</button>
    <!-- 购买的数量 -->
    <span class="number-box">{{ count }}</span>
    <!-- 加 1 的按钮 -->
    <button type="button" class="btn btn-light btn-sm" @click="add">+</button>
  </div>
</template>

<script>
import bus from "@/eventBus.js";
export default {
  props: {
    count: {
      default: 1,
      type: Number,
    },
    id: {
      type: Number,
      required: true,
    },
  },
  methods: {
    add() {
      const obj = { id: this.id, value: this.count + 1 };
      bus.$emit("share", obj);
    },
    minus() {
      if (this.count > 1) {
        const obj = { id: this.id, value: this.count - 1 };
        bus.$emit("share", obj);
      }
    },
  },
};
</script>

<style lang="less" scoped>
.number-box {
  min-width: 30px;
  text-align: center;
  margin: 0 5px;
  font-size: 12px;
}

.btn-sm {
  width: 30px;
}
</style>
