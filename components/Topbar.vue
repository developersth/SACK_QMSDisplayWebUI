<template>
    <div>
        <v-app-bar color="primary" app dark>
            <nuxt-link to="/">
                <img class="mr-4" src="~assets/images/logo.png" alt="logo" height="50" />
            </nuxt-link>
            <v-app-bar-title class="text-center">Queue Management System</v-app-bar-title>
            <v-spacer></v-spacer>
            <v-tooltip v-if="!$vuetify.theme.dark" bottom>
                <template v-slot:activator="{ on }">
                    <v-btn v-on="on" color="info" small fab @click="toggleTheme">
                        <v-icon class="mr-1">mdi-moon-waxing-crescent</v-icon>
                    </v-btn>
                </template>
                <span>Dark Mode On</span>
            </v-tooltip>

            <v-tooltip v-else bottom>
                <template v-slot:activator="{ on }">
                    <v-btn v-on="on" color="info" small fab @click="toggleTheme">
                        <v-icon color="yellow">mdi-white-balance-sunny</v-icon>
                    </v-btn>
                </template>
                <span>Dark Mode Off</span>
            </v-tooltip>
        </v-app-bar>
    </div>
</template>

<script>
export default {
    data() {
        return {
            swtheme: false
        }
    },
    methods: {
        toggleTheme() {
            this.$vuetify.theme.dark = !this.$vuetify.theme.dark
            localStorage.setItem('dark_theme', this.$vuetify.theme.dark.toString())
        },
    },
    mounted() {
        const theme = localStorage.getItem('dark_theme')
        if (theme) {
            if (theme == 'true') {
                this.$vuetify.theme.dark = true
                this.swtheme = true
            } else {
                this.$vuetify.theme.dark = false
                this.swtheme = false
            }
        }
    },
}
</script>

<style></style>