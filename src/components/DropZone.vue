<script>
export default {
    emits: ["file-dropped"],
    methods: {
        onDrop (e) {
            this.$emit("file-dropped", [...e.dataTransfer.files]);
        },
        selectedFiles() {
            this.$emit("file-dropped", [...this.$refs.file.files]);
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
        document.body.removeEventListener(eventName, this.preventDefaults)
        })
    },
}

</script>

<template>
    <div 
        @drop.prevent="onDrop" 
        class="box"
    >
        <h1 
            class="is-size-1 
                has-text-centered 
                has-text-weight-bold 
                primary-text-color"
        >
                Drag and drop images here
        </h1>
        <div class="buttons are-large is-centered">
            
            <button 
                class="button 
                    is-full-width 
                    is-rounded 
                    box-button" 
            >
                <label 
                    class="file-label file-style" 
                >
                    <input 
                        ref="file" 
                        @change="selectedFiles" 
                        class="file-input file-style" 
                        type="file" 
                        multiple 
                    >
                    <p 
                        class="primary-text-color has-text-weight-semibold" 
                        style="margin: auto auto;"
                    >
                    Browse files
                    </p>
                </label>
            </button>

            <slot></slot>

        </div>
    </div>
</template>

<style scoped>

.button {
    padding: 0px 0px;
    width: 90%;
}

.file-style {
    width: 100%;
    height: 100%;
    cursor: pointer;
    text-align: center;
}

</style>