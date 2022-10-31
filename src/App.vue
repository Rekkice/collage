<script>
import { RouterLink, RouterView } from 'vue-router'
export default {
    data() {
        return {
            images: Array,
        }
    },
    methods: {
        updateImages(images) {
            this.images = images;
        }
    }
}
</script>

<template>
<RouterView :images="images" @image-change="(images) => updateImages(images)" v-slot="{Component}" id="router-view">
    <transition name="slide" mode="out-in">
        <component :is="Component" />
    </transition>
</RouterView>
</template>

<style>

#router-view {
    height: 100%;
    width: 100%;
    top: 0px;
    left: 0px;
}

.slide-enter-active,
.slide-leave-active{
  transition: opacity 1s, transform 1s;
}

.slide-enter-from,
.slide-leave-to{
    opacity:0;
    transform: translateX(-30%);
}
</style>