<template>
    <v-row justify="center" align="center">
        <v-col cols="12" sm="8" md="6">
            <v-card>
                <v-card-title class="headline">
                    Welcome to the Vuetify + Nuxt.js Dropzone
                </v-card-title>
                <v-card-subtitle>
                    Drag and drop functionalites for the file upload in form,
                    purely based on vuetify :)
                </v-card-subtitle>
                <v-card-text>
                    <Dropzone v-model="file" />
                    <div class="">Props usage details:</div>
                    <div><code>v-model:</code> for storing file.</div>
                    <div>
                        <code>size:</code> specify the file upload size, default
                        is 5MB.
                    </div>
                </v-card-text>
            </v-card>
        </v-col>
    </v-row>
</template>

<script>
export default {
    data: () => ({
        file: null,
    }),
    mounted() {
        this.$toast.success("Successfully authenticated");
    },
};
</script>
