<template>
    <v-app dark>
        <v-app-bar fixed app>
            <v-toolbar-title v-text="title" />
        </v-app-bar>

        <v-main>
            <v-container>
                <Nuxt />
            </v-container>
        </v-main>

        <v-footer app>
            Vuetify dropzone <span>&copy; {{ new Date().getFullYear() }}</span>
        </v-footer>
    </v-app>
</template>

<script>
export default {
    data() {
        return {
            title: "Vuetify Dropzone",
        };
    },
};
</script>
