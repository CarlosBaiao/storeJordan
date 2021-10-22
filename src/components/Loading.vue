<template>
  <div class="loading">

  </div>
</template>

<script>
export default {

}
</script>

<style lang="less" scoped>
    .loading {
        width: 50px;
        height: 50px;
        border: 3px solid @light-blue;
        border-radius: 50%;
        border-top-color: @blue;
        animation: spin 1s linear infinite;
        margin: 100px auto;
    }

    @keyframes spin {
        to{
            transform: rotate(360deg);
        }
    }
</style>