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

<style scoped>
.delete {
    position: absolute;
    top: 10px;
    right: 10px;
}

.image-name {
    word-break: break-all;
    margin: -20px 0 -20px 0;
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
    overflow-y: auto;
    overflow-x: hidden;
}

.panel-heading {
    margin: -10px -10px 5px -10px;
}

.notification {
    margin: -5px 0px -5px 0px; 
    max-height: 10%; 
    width: 100%;
}

img {
    margin: -5px 0 -22px 0;
}
</style>

<template>
    <section class="panel current-files is-primary">
        <h1 
            class="panel-heading is-size-3 has-text-centered"
        >
        Current files
        </h1>

        <transition-group 
            name="list" 
            tag="p"
        >
        <a 
            v-for="fileImage in currentFiles" 
            class="panel-block" 
            :key="fileImage"
        >
            <div 
                class="notification is-primary"
            >
                <button 
                    class="delete" 
                    @click="deleteButton(fileImage)"
                ></button>

                <h1 
                    class="image-name is-family-primary"
                >
                    {{fileImage.name}}
                </h1><br>

                <img 
                    :src="getUrl(fileImage)" 
                    width="50" 
                    height="50"
                >

            </div>
        </a>
        </transition-group>

    </section>
</template>