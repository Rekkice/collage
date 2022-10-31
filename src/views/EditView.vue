<script>
export default {
    props: {
        images: Array,
    },
    mounted() {
        console.log(this.images);
    }
}
</script>

<template>
<div style="display: flex; align-items: center; justify-content: center;">
  <div class="box" style="height: 90%; width: 90%;">
    Test
  </div>
</div>
</template>

<style>

</style>