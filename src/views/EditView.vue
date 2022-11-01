<script>
import CanvasCom from "../components/CanvasCom.vue"
export default {
    data() {
        return {
            canvasBind: null,
        }
    },
    components: {
        CanvasCom
    },
    props: {
        images: Array,
    },
    mounted() {
        const box = this.$refs.box.getBoundingClientRect();

        const padding = 40;
        this.canvasBind = {"height":box.height - padding, "width":box.width - padding};

        this.$refs.box.height = this.canvasBind.height;
        this.$refs.box.width = this.canvasBind.width;
    },
}
</script>

<template>
<div style="display: flex; align-items: center; justify-content: center;">
  <div ref="box" class="box main-box">
    <CanvasCom v-if="canvasBind != null" :images="images" :canvas-bind="canvasBind"></CanvasCom>
  </div>
</div>
</template>

<style>
.main-box {
    height: 90%;
    width: 90%;
}
</style>