<template>
<div>
    <!-- sidebar -->
    <v-navigation-drawer v-model="drawer" app fixed temporary>
        <v-list>
            <v-container justify-center>
                <v-btn flat to="/" style="cursor: pointer">
                <v-icon class="mr-1">free_breakfast</v-icon>TEN</v-btn>
                <v-flex>
                <v-btn flat to="portfolio" style="cursor: pointer">
                    <v-icon left>assessment</v-icon>Portfolio</v-btn>
                </v-flex>
                <v-flex>
                    <LoginDialog></LoginDialog>
                </v-flex>
            </v-container>
        </v-list>
    </v-navigation-drawer>
    <!-- end sidebar -->
    <!-- #112d4e-->
    <!-- navbar -->
    <v-toolbar color='#248ea9' fixed app temporary dark scroll-off-screen>
        <v-toolbar-side-icon @click.stop="drawer = !drawer" class="hidden-sm-and-up">
            <v-icon>fa-bars</v-icon>
        </v-toolbar-side-icon>
        <v-toolbar-title>
            <router-link to="/" tag="span" style="cursor: pointer">
                <v-icon class="mr-1">free_breakfast</v-icon>TEN</router-link>
        </v-toolbar-title>
        <TranslateBtn></TranslateBtn>
        <v-spacer></v-spacer>
        <v-toolbar-items class="hidden-xs-only">
            <v-btn flat to="portfolio">
                <v-icon left>assessment</v-icon>Portfolio</v-btn>
            <LoginDialog></LoginDialog>
            
        </v-toolbar-items>
    </v-toolbar>
    <!-- end navbar -->

    <!-- backTotop button -->
    <v-fab-transition>
        <v-btn v-show="fab" v-scroll="onScroll" class="md-5 mr-3 elevation-21" fab fixed bottom right color="#aee7e8" @click="toTop">
            <v-icon color="#248ea9">keyboard_arrow_up</v-icon>
        </v-btn>
    </v-fab-transition>
    <!-- end backTotop button -->
</div>
</template>

<script>
import TranslateBtn from './TranslateBtn'
import LoginDialog from '@/components/LoginDialog'
export default {
    name: 'Header',
    data() {
        return {
            fab: false,
            drawer: false
        }
    },
    components: {
        TranslateBtn,
        LoginDialog
    },
    methods: {
        onScroll() {
            if (typeof window === 'undefined') return
            const top = window.pageYOffset ||
                document.documentElement.offsetTop ||
                0
            this.fab = top > 300
        },
        toTop() {
            this.$router.push({
                hash: ''
            })
            this.$vuetify.goTo(0)
            behavior: "smooth"
        }

    }

}
</script>

<style scoped>

</style>
