<template>
    <v-app dark>
        <v-toolbar app>
            <v-toolbar-title class="headline">
                <span class="font-weight-light">DoomTrain</span>
            </v-toolbar-title>
        </v-toolbar>
        <v-content class="main">
            <MainPage></MainPage>
        </v-content>
    </v-app>
</template>

<script>

    import MainPage from "./pages/MainPage";

    export default {
        name: 'App',
        components: {
            MainPage
        }
    }
</script>

<style scoped>
    .main {
        margin: 5%;
    }
</style>
