<template>
  <div class="header">
    <h1>Tudo List</h1>
  </div>
</template>

<script>
export default {
  name: "HeaderList",
};
</script>

<style scoped lang="less">
@import url("https://fonts.googleapis.com/css2?family=Permanent+Marker&display=swap");

.header {
  width: 100%;
  height: 250px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: url(../assets/cidade.jpg);
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 50% 45%;

  h1 {
    margin: 0;
    font-size: 4rem;
    color: @orange;
    font-weight: 400;
    background: rgba(0, 0, 0, 0.6);
    padding: 30px 60px;
    border-radius: 20px;
    font-family: "Permanent Marker", cursive;
  }

  @media @tablets {
    h1 {
      font-size: 2.5rem;
    }
  }

  @media @smartphones {
    h1 {
      font-size: 2rem;
    }
  }
}
</style>
