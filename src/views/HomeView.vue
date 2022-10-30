<script>
import DropZone from '../components/DropZone.vue'
export default {
    data() {
        return {
            droppedFiles: Array(),
            url: null
        }
    },
    components: {
        DropZone,
    },
    methods: {
        gotFiles(files) {
            let filteredFiles = files.filter(file => file.type.includes('image'));
            this.droppedFiles = this.droppedFiles.concat(filteredFiles);
            console.log("got files");
        },
        getUrl(image) {
            return URL.createObjectURL(image);
        },
    }
}
</script>

<style>
.column {
    height:80vh;
}
.current-files {
    padding-left: 5px;
    overflow-y: auto;
}
.image-name {
    word-break: break-all;
    margin: -10px 0 -20px 0;
    color: rgb(252, 224, 224);
}

.primary-text-color {
    color: rgb(122, 56, 56);
}
</style>

<template>

<div class="columns is-centered" style="width: 90vw">

    <DropZone class="column is-three-quarters" style="margin: 0 10px 0 0;" @file-dropped="(files) => gotFiles(files)">
        <h1 class="is-size-1 has-text-centered has-text-weight-bold primary-text-color">
            Drag and drop images here
        </h1>
    </DropZone>


    <section class="panel current-files column is-one-quarter is-primary">
        <h1 class="panel-heading is-size-3 has-text-centered" style="margin: -10px -10px 5px -10px;">Current files</h1>

        <a class="panel-block" v-for="fileImage in droppedFiles">
            <div class="notification is-primary" style="margin: -5px 0 -5px 0; max-height: 10%; width: 100%;">
                <h1 class="image-name is-family-primary" style="margin: -20px 0 -20px 0;">
                    {{fileImage.name}}
                </h1><br>
                <img :src="getUrl(fileImage)" width="50" height="50" style="margin: -5px 0 -20px 0;">
            </div>
        </a>
    </section>
</div>

</template>