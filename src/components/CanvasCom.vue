<script>
import {fabric} from "fabric"
export default {
    data() {
        return {
            fabricCanvas: null,
            drawnObjects: [],
        }
    },
    props: {
        images: Array,
        canvasBind: Object,
    },
    methods: {

    },
    mounted() {
        let canvas = new fabric.Canvas("canvas");
        this.fabricCanvas = canvas;
        for (let i = 0; i < this.images.length; i++) {
            let url = URL.createObjectURL(this.images[i]);
            fabric.Image.fromURL(url, function(oImg) {
                oImg.set({
                    left: 200 * (i + 1),
                    top: 100,
                });
                oImg.scaleToWidth(300, false);
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