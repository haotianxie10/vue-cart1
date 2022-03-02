<template>
  <div class="header-container">
    <img class="logo1" src="@/assets/logo1.png" alt="" />
  </div>
</template>

<script>
export default {};
</script>

<style lang="less" scoped>
.header-container {
  font-size: 12px;
  height: 45px;
  width: 100%;
  background-color: #3a3230;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
  position: fixed;
  top: 0;
  z-index: 999;
}
.logo1 {
  height: 45px;
}
</style>
