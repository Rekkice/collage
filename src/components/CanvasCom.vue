<script>
import {fabric} from "fabric"
export default {
    emits: ["canvas"],
    data() {
        return {
            fabricCanvas: null,

        }
    },
    props: {
        images: Array,
        canvasBind: Object,
    },
    methods: {

    },
    mounted() {
        let canvas = new fabric.Canvas("canvas", {
            backgroundColor: "rgb(255, 221, 221)",
        });
        this.$emit("canvas", canvas);
        this.fabricCanvas = canvas;
        let maxWidth = this.canvasBind.width;
        let maxHeight = this.canvasBind.height;
        for (let i = 0; i < this.images.length; i++) {
            let url = URL.createObjectURL(this.images[i]);
            fabric.Image.fromURL(url, function(oImg) {
                oImg.set({
                    left: 10 + ((200 * i) % maxWidth),
                    top: (200 * Math.floor((200 * i) / maxWidth)) % (maxHeight - 100),
                    borderColor: "rgb(245, 134, 134)",
                    cornerColor: "rgb(122, 56, 56)",
                    stroke: 'rgb(245, 134, 134)',
                    strokeWidth: 10,
                    strokeUniform: true,
                });
                oImg.scaleToWidth(200, false);
                oImg.setControlsVisibility({ mtr: false, ml: false , mr: false, mt: false, mb: false});
                canvas.add(oImg);
            });
        }
    },
}
</script>

<script>


</script>

<template>
<canvas id="canvas" v-bind="canvasBind" />
</template>

<style>
#canvas {
    display:block;
    border: 6px double rgb(245, 134, 134);
    border-radius: 5px;
}
</style>