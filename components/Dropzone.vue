<template>
    <v-card elevation="0" class="my-2">
        <v-card-text
            v-if="!file"
            :class="['dropZone', 'py-3', dragging ? 'overlay' : '']"
            @dragenter="dragging = true"
            @dragleave="dragging = false"
        >
            <div class="d-flex justify-center" @drag="onChange">
                <v-icon large left>mdi-cloud-upload-outline</v-icon>
                <span>
                    Drop file or click to upload
                    <br />
                    Maximum file size: {{ size }}MB
                </span>
            </div>
            <input type="file" @change="onChange" />
        </v-card-text>

        <v-card-text v-else class="dropZone">
            <div class="d-flex">
                <v-icon x-large left>mdi-file-outline</v-icon>
                <span class="ml-3">
                    <div>
                        File name: {{ file.name }}
                        <br />
                        Size: {{ calculateFileSize(file.size) }}
                    </div>
                    <v-btn color="error" x-small @click="removeFile">
                        Remove
                    </v-btn>
                </span>
                <v-icon right class="ml-auto success--text">
                    mdi-cloud-check-outline
                </v-icon>
            </div>
        </v-card-text>
    </v-card>
</template>

<script>
export default {
    name: "DropZone",
    props: {
        size: {
            type: Number,
            default: 5,
        },
    },
    data() {
        return {
            file: "",
            dragging: false,
        };
    },
    methods: {
        calculateFileSize(size) {
            return (size / 1000000).toFixed(2) + "MB";
        },

        onChange(e) {
            const files = e.target.files || e.dataTransfer.files;

            if (!files.length) {
                this.dragging = false;
                return;
            }

            this.createFile(files[0]);
        },
        createFile(file) {
            if (file.size > this.size * 1000000) {
                alert("please check file size no over 5 MB.");
                this.dragging = false;
                return;
            }

            this.file = file;
            this.dragging = false;
            this.$emit("input", this.file);
        },
        removeFile() {
            this.file = "";
        },
    },
};
</script>

<style scoped lang="scss">
.dropZone {
    position: relative;
    border: 5px dashed #eee;
    &:hover {
        border: 5px dashed #2e94c4;
    }
    .overlay {
        background: #5c5c5c;
        opacity: 0.8;
    }
}

.dropZone input {
    position: absolute;
    cursor: pointer;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 100%;
    opacity: 0;
}
</style>