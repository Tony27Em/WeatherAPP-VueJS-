<script>
export default {
  data() {
    return {}
  },
}
</script>

<template>
  <div class="error">
    <img class="error-img" src="../assets/error.png">
    <p class="error-message">Oops! Nothing found <br><br> Try again</p>
  </div>
</template>

<style lang="scss">
.error {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 25px;
  text-align: center;
  overflow: hidden;
  margin: 100px 0;

  &-message {
    font-size: 2em;
  }
}
</style>