<script>
export default {
emits: ["file-dropped"],
    methods: {
        onDrop (e) {
            this.$emit("file-dropped", [...e.dataTransfer.files]);
        },
        preventDefaults(e) {
            e.preventDefault()
        },
    },

    mounted() {
        const events = ['dragenter', 'dragover', 'dragleave', 'drop'];
        events.forEach((eventName) => {
            document.body.addEventListener(eventName, this.preventDefaults)
        })
    },

    unmounted() {
        const events = ['dragenter', 'dragover', 'dragleave', 'drop'];
        events.forEach((eventName) => {
        document.body.removeEventListener(eventName, preventDefaults)
        })
    },
}

</script>

<template>
    <div @drop.prevent="onDrop" class="box">
      <slot></slot>
    </div>
</template>

<style>

</style>