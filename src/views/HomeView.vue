<script>
import DropZone from '../components/DropZone.vue'
import CurrentFiles from '../components/CurrentFiles.vue'
export default {
    emits: ["image-change"],
    data() {
        return {
            droppedFiles: Array(),
        }
    },
    components: {
        DropZone,
        CurrentFiles,
    },
    methods: {
        gotFiles(files) {
            let filteredFiles = files.filter(file => file.type.includes('image'));
            this.droppedFiles = this.droppedFiles.concat(filteredFiles);
            this.$emit("image-change", this.droppedFiles);
        },
        deleteImage(image) {
            this.droppedFiles = this.droppedFiles.filter(x => x !== image);
            this.$emit("image-change", this.droppedFiles);
        },
    },
    computed: {
        buttonIsDisabled() {
            if (this.droppedFiles.length > 0) return false;
            return true;
        },
    }
}
</script>

<style>
.column {
    height: 85%;
    margin-left: 10px;
}

.box-button {
    margin: 10px 0 0 0;
    display: block;
    width: 90%;
}

</style>

<template>

<div class="columns is-vcentered is-centered" style="margin: 0 auto; width: 90%;">

    <DropZone class="column is-three-quarters is-flex is-flex-direction-column is-justify-content-space-between" 
        @file-dropped="(files) => gotFiles(files)" style="margin-bottom: 0;">

        <router-link
        images="droppedFiles"
        class="box-button"
        to="/edit"
        v-slot="{href, navigate}"
        >
            <button :href="href" @click="navigate" class='button is-full-width is-rounded' style="width: 100%" :disabled="buttonIsDisabled">
                <p class="primary-text-color has-text-weight-semibold">Next</p>
            </button>
        </router-link>

    </DropZone>

    <CurrentFiles class="column is-one-quarter" :currentFiles="droppedFiles" @delete-button="(image) => deleteImage(image)"/>
    
</div>

</template>