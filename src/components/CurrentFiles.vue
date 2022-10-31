<script>
export default {
    emits: ["deleteButton"],
    props: {
        currentFiles: Array,
    },
    methods: {
        getUrl(image) {
            return URL.createObjectURL(image);
        },
        deleteButton(image) {
            this.$emit("deleteButton", image);
        }
    }
}
</script>

<style>
.delete {
    position: absolute;
    top: 10px;
    right: 10px;
}

.image-name {
    word-break: break-all;
    margin: -10px 0 -20px 0;
    color: rgb(252, 224, 224);
}

.list-item {
  display: inline-block;
  margin-right: 0px;
}
.list-enter-active, .list-leave-active {
  transition: all 0.3s;
}
.list-enter, .list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
.current-files {
    /* padding-left: 5px; */
    overflow-y: auto;
    overflow-x: hidden;
}
</style>

<template>
    <section class="panel current-files is-primary">
        <h1 class="panel-heading is-size-3 has-text-centered" style="margin: -10px -10px 5px -10px;">Current files</h1>

        <transition-group name="list" tag="p">
        <a v-for="fileImage in currentFiles" class="panel-block" :key="fileImage">
            <div class="notification is-primary" style="margin: -5px 0 -5px 0; max-height: 10%; width: 100%;">
                <button class="delete" @click="deleteButton(fileImage)"></button>
                <h1 class="image-name is-family-primary" style="margin: -20px 0 -20px 0;">
                    {{fileImage.name}}
                </h1><br>
                <img :src="getUrl(fileImage)" width="50" height="50" style="margin: -5px 0 -20px 0;">
            </div>
        </a>
        </transition-group>

    </section>
</template>