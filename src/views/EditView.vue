<script>
import CanvasCom from "../components/CanvasCom.vue"
export default {
    data() {
        return {
            canvasBind: null,
            canvas: null,
            href: null,
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
    methods: {
        gotCanvas(canvas) {
            this.canvas = canvas;
        },
        saveImage() {
            this.href = this.canvas.toDataURL({format: 'png'});
        }
    },
    computed: {
        getHref() {
            if (this.canvas == null) return "";
            return this.canvas.toDataURL({format: 'png'});
        },
    }
}
</script>

<template>
<div class="main-div">
    <div 
        ref="box" 
        class="box main-box"
    >
    <CanvasCom 
        v-if="canvasBind != null" 
        :images="images" 
        :canvas-bind="canvasBind" 
        @canvas="(canvas) => gotCanvas(canvas)"
    >
    </CanvasCom>
    </div>
    <a class="button 
            is-full-width 
            is-rounded 
            is-large"
        @click="saveImage" 
        :href="href" 
        download="canvas.png" 
    > 
        <h1 class="primary-text-color is-family-primary">
            Download
        </h1>
    </a>
</div>
</template>

<style scoped>
.main-box {
    height: 90%;
    width: 90%;
    margin-top: 10px;
}

.main-div {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
}

.button {
    margin-bottom: 1.5rem;
    width: 60%;
}
</style>