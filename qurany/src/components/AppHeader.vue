<template>
  <header class="navbar">
    <h1>
      <img :src="logoSrc" alt="headphone logo" class="img-logo" />
      <span>Qurany</span>
    </h1>
  </header>
</template>

<script>
export default {
  name: "AppHeader",
  data: function() {
    return {
      logoSrc: require("./../assets/images/headphones.png")
    };
  }
};
</script>

<style scoped>
header {
  text-align: center;
}
.navbar {
  height: 80px;
  margin: 0 auto;
}

.navbar h1 {
  color: #fff;
  padding-top: 50px;
  padding-bottom: 20px;
  letter-spacing: 5px;
  font-family: "Courier New", Courier, monospace;
  font-size: 65px;
}

.img-logo {
  width: 55px;
  margin-right: 20px;
}
</style>