<template>
    <div class="mb-3">
        <input class="form-control" ref="fileInput" type="file" @input="pickFile" accept=".jpg, .png">
    </div>
    <div class="imagePreviewWrapper" :style="{ 'background-image': `url(${previewImage})` }" @click="selectImage"></div>
</template>
<script>
export default {
    data() {
        return {
            previewImage: null
        }
    },
    methods: {
        //image upload and preview methods
        selectImage() {
            this.$refs.fileInput.click()
        },
        pickFile() {
            let input = this.$refs.fileInput
            let file = input.files
            if (file && file[0]) {
                let reader = new FileReader
                reader.onload = e => {
                    this.previewImage = e.target.result
                }
                reader.readAsDataURL(file[0])
                this.$emit('input', file[0])
            }
        }
    },
}
</script>
<style scoped>
.imagePreviewWrapper {
    background-repeat: no-repeat;
    width: 250px;
    height: 250px;
    display: block;
    cursor: pointer;
    margin: 0 auto 30px;
    background-size: contain;
    background-position: center center;
}
</style>